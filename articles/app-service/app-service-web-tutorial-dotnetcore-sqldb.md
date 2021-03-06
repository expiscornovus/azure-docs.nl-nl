---
title: Een .NET Core- en SQL Database-web-app maken in Azure App Service | Microsoft Docs
description: Informatie over het verkrijgen van een .NET Core-app die in Azure App Service werkt, met verbinding aan een SQL-database.
services: app-service\web
documentationcenter: dotnet
author: cephalin
manager: syntaxc4
editor: 
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: tutorial
ms.date: 01/23/2018
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 1a60c76b2687e4c6561eabf8a19dbfffffbe8681
ms.sourcegitcommit: 9d317dabf4a5cca13308c50a10349af0e72e1b7e
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 02/01/2018
---
# <a name="build-a-net-core-and-sql-database-web-app-in-azure-app-service"></a>Een .NET Core- en SQL Database-web-app maken in Azure App Service

> [!NOTE]
> In dit artikel gaat u een app implementeren in App Service onder Windows. Zie [Een .NET Core- en SQL Database-web-app maken in Azure App Service op Linux](./containers/tutorial-dotnetcore-sqldb-app.md) als u naar App Service wilt implementeren op _Linux_.
>

[App Servicex](app-service-web-overview.md) biedt een uiterst schaalbare webhostingservice met self-patchfunctie in Azure. In deze zelfstudie wordt getoond hoe u een .NET Core-app maakt en verbinding laat maken met een SQL-database. Als u klaar bent, hebt u een .NET Core MVC-app die in App Service wordt uitgevoerd.

![app die in App Service wordt uitgevoerd](./media/app-service-web-tutorial-dotnetcore-sqldb/azure-app-in-browser.png)

U leer het volgende:

> [!div class="checklist"]
> * Een SQL-database in Azure maken
> * Een .NET Core-app verbinden met SQL Database
> * De app implementeren in Azure
> * Het gegevensmodel bijwerken en de app opnieuw implementeren
> * Logboeken met diagnostische gegevens vanaf Azure streamen
> * De app in Azure Portal beheren

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="prerequisites"></a>Vereisten

Vereisten voor het voltooien van deze zelfstudie:

1. [Git installeren](https://git-scm.com/)
1. [.NET Core SDK 1.1.2 installeren](https://github.com/dotnet/core/blob/master/release-notes/download-archives/1.1.2-download.md)

## <a name="create-local-net-core-app"></a>Lokale .NET Core-app maken

In deze stap stelt u het lokale .NET Core-project in.

### <a name="clone-the-sample-application"></a>De voorbeeldtoepassing klonen

In het terminalvenster, `cd` in een werkmap.

Voer de volgende opdrachten uit om de voorbeeldopslagplaats te klonen en de hoofdmap ervan te wijzigen.

```bash
git clone https://github.com/azure-samples/dotnetcore-sqldb-tutorial
cd dotnetcore-sqldb-tutorial
```

Het voorbeeldproject bevat een eenvoudige CRUD-app (create-read-update-delete) die gebruikmaakt van [Entity Framework Core](https://docs.microsoft.com/ef/core/).

### <a name="run-the-application"></a>De toepassing uitvoeren

Voer de volgende opdrachten uit om de vereiste pakketten te installeren, databasemigraties uit te voeren en de toepassing te starten.

```bash
dotnet restore
dotnet ef database update
dotnet run
```

Ga naar `http://localhost:5000` in een browser. Selecteer de koppeling **Nieuwe maken** en maak enkele _taakitems_.

![is verbonden met SQL Database](./media/app-service-web-tutorial-dotnetcore-sqldb/local-app-in-browser.png)

Als u .NET Core wilt stoppen, drukt u in de terminal op `Ctrl+C`.

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

## <a name="create-production-sql-database"></a>SQL-productiedatabase maken

In deze stap maakt u een SQL-database in Azure. Als de app is geïmplementeerd in Azure, wordt deze cloud-database gebruikt.

Voor SQL Database wordt in deze zelfstudie gebruikgemaakt van [Azure SQL Database](/azure/sql-database/).

### <a name="create-a-resource-group"></a>Een resourcegroep maken

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group-no-h.md)]

### <a name="create-a-sql-database-logical-server"></a>Een logische SQL Database-server maken

Maak een logische Azure SQL Database-server in Cloud Shell met de opdracht [`az sql server create`](/cli/azure/sql/server?view=azure-cli-latest#az_sql_server_create).

Vervang de tijdelijke aanduiding *\<server_name>* door een unieke SQL Database-naam. Deze naam wordt gebruikt als onderdeel van het SQL Database-eindpunt, `<server_name>.database.windows.net`. De naam moet dus uniek zijn voor alle logische servers in Azure. De naam mag alleen kleine letters, cijfers en het afbreekstreepje (-) bevatten, en moet tussen de 3 en 50 tekens lang zijn. Vervang tevens *\<db_username>* en *\<db_password>* door een gebruikersnaam en wachtwoord dat u zelf mag kiezen. 


```azurecli-interactive
az sql server create --name <server_name> --resource-group myResourceGroup --location "West Europe" --admin-user <db_username> --admin-password <db_password>
```

Wanneer de logische SQL Database-server wordt gemaakt, toont de Azure CLI informatie die lijkt op het volgende voorbeeld:

```json
{
  "administratorLogin": "sqladmin",
  "administratorLoginPassword": null,
  "fullyQualifiedDomainName": "<server_name>.database.windows.net",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Sql/servers/<server_name>",
  "identity": null,
  "kind": "v12.0",
  "location": "westeurope",
  "name": "<server_name>",
  "resourceGroup": "myResourceGroup",
  "state": "Ready",
  "tags": null,
  "type": "Microsoft.Sql/servers",
  "version": "12.0"
}
```

### <a name="configure-a-server-firewall-rule"></a>Een serverfirewallregel configureren

Maak [Een firewallregel op serverniveau voor Azure SQL Database](../sql-database/sql-database-firewall-configure.md) met de opdracht [`az sql server firewall create`](/cli/azure/sql/server/firewall-rule?view=azure-cli-latest#az_sql_server_firewall_rule_create). Als zowel het IP-beginadres als het IP-eindadres zijn ingesteld op 0.0.0.0, wordt de firewall alleen geopend voor andere Azure-resources. 

```azurecli-interactive
az sql server firewall-rule create --resource-group myResourceGroup --server <server_name> --name AllowYourIp --start-ip-address 0.0.0.0 --end-ip-address 0.0.0.0
```

### <a name="create-a-database"></a>Een database maken

Maak een database met een [prestatieniveau van S0](../sql-database/sql-database-service-tiers.md) op de server met de opdracht [`az sql db create`](/cli/azure/sql/db?view=azure-cli-latest#az_sql_db_create).

```azurecli-interactive
az sql db create --resource-group myResourceGroup --server <server_name> --name coreDB --service-objective S0
```

### <a name="create-connection-string"></a>Verbindingsreeks maken

Vervang de volgende reeks door de waarden *\<server_name>*, *\<db_username>* en *\<db_password>* die u eerder hebt gebruikt.

```
Server=tcp:<server_name>.database.windows.net,1433;Initial Catalog=coreDB;Persist Security Info=False;User ID=<db_username>;Password=<db_password>;MultipleActiveResultSets=False;Encrypt=True;TrustServerCertificate=False;Connection Timeout=30;
```

Dit is de verbindingsreeks voor uw app .NET Core-app. Kopieer deze voor later gebruik.

## <a name="deploy-app-to-azure"></a>App in Azure implementeren

In deze stap implementeert u de met SQL Database verbonden .NET Core-app met App Service.

### <a name="configure-local-git-deployment"></a>Lokale Git-implementatie configureren

[!INCLUDE [Configure a deployment user](../../includes/configure-deployment-user-no-h.md)]

### <a name="create-an-app-service-plan"></a>Een App Service-plan maken

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan-no-h.md)]

### <a name="create-a-web-app"></a>Een webtoepassing maken

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app-dotnetcore-win-no-h.md)] 

### <a name="configure-an-environment-variable"></a>Een omgevingsvariabele configureren

Als u verbindingsreeksen voor de Azure-app wilt instellen, gebruikt u de opdracht [`az webapp config appsettings set`](/cli/azure/webapp/config/appsettings?view=azure-cli-latest#az_webapp_config_appsettings_set) in Cloud Shell. In de volgende opdracht vervangt u *\<app name>* en de parameter *\<connection_string>* door de eerder gemaakte verbindingsreeks.

```azurecli-interactive
az webapp config connection-string set --resource-group myResourceGroup --name <app name> --settings MyDbConnection='<connection_string>' --connection-string-type SQLServer
```

Vervolgens stelt u de instelling voor `ASPNETCORE_ENVIRONMENT`-app in op _Productie_. Deze instelling betekent dat u de app in Azure uitvoert omdat u SQLite gebruikt voor uw lokale ontwikkelomgeving en SQL Database voor uw Azure-omgeving.

In het volgende voorbeeld wordt een `ASPNETCORE_ENVIRONMENT`-app-instelling in de Azure-web-app geconfigureerd. Vervang de tijdelijke aanduiding *\<app_name>*.

```azurecli-interactive
az webapp config appsettings set --name <app_name> --resource-group myResourceGroup --settings ASPNETCORE_ENVIRONMENT="Production"
```

### <a name="connect-to-sql-database-in-production"></a>Verbinding maken met SQL Database in productie

Open Startup.cs in de lokale opslagplaats en zoek de volgende code:

```csharp
services.AddDbContext<MyDatabaseContext>(options =>
        options.UseSqlite("Data Source=localdatabase.db"));
```

Vervang deze door de volgende code, waarin de omgevingsvariabelen worden gebruikt die u eerder hebt geconfigureerd.

```csharp
// Use SQL Database if in Azure, otherwise, use SQLite
if(Environment.GetEnvironmentVariable("ASPNETCORE_ENVIRONMENT") == "Production")
    services.AddDbContext<MyDatabaseContext>(options =>
            options.UseSqlServer(Configuration.GetConnectionString("MyDbConnection")));
else
    services.AddDbContext<MyDatabaseContext>(options =>
            options.UseSqlite("Data Source=MvcMovie.db"));

// Automatically perform database migration
services.BuildServiceProvider().GetService<MyDatabaseContext>().Database.Migrate();
```

Als met deze code wordt gedetecteerd dat deze in productie wordt uitgevoerd (wat op de Azure-omgeving wijst), wordt de verbindingsreeks gebruikt die u hebt geconfigureerd om verbinding te maken met SQL Database.

De `Database.Migrate()`-aanroep helpt u wanneer deze in Azure wordt uitgevoerd, omdat automatisch de database wordt gemaakt die nodig is voor de NET Core-app, op basis van de migratieconfiguratie. 

Sla uw wijzigingen op en voor deze door naar de Git-opslagplaats. 

```bash
git commit -am "connect to SQLDB in Azure"
```

### <a name="push-to-azure-from-git"></a>Pushen naar Azure vanaf Git

[!INCLUDE [app-service-plan-no-h](../../includes/app-service-web-git-push-to-azure-no-h.md)]

```bash
Counting objects: 98, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (92/92), done.
Writing objects: 100% (98/98), 524.98 KiB | 5.58 MiB/s, done.
Total 98 (delta 8), reused 0 (delta 0)
remote: Updating branch 'master'.
remote: .
remote: Updating submodules.
remote: Preparing deployment for commit id '0c497633b8'.
remote: Generating deployment script.
remote: Project file path: ./DotNetCoreSqlDb.csproj
remote: Generated deployment script files
remote: Running deployment command...
remote: Handling ASP.NET Core Web Application deployment.
remote: .
remote: .
remote: .
remote: Finished successfully.
remote: Running post deployment command(s)...
remote: Deployment successful.
remote: App container will begin restart within 10 seconds.
To https://<app_name>.scm.azurewebsites.net/<app_name>.git
 * [new branch]      master -> master
```

### <a name="browse-to-the-azure-web-app"></a>Bladeren naar de Azure-web-app

Blader naar de geïmplementeerde web-app via uw webbrowser.

```bash
http://<app_name>.azurewebsites.net
```

Voeg enkele taakitems toe.

![app die in App Service wordt uitgevoerd](./media/app-service-web-tutorial-dotnetcore-sqldb/azure-app-in-browser.png)

**Gefeliciteerd!** U voert een gegevensgestuurde .NET Core-app uit in App Service.

## <a name="update-locally-and-redeploy"></a>Lokaal bijwerken en opnieuw implementeren

In deze stap wijzigt u het databaseschema en publiceert u het in Azure.

### <a name="update-your-data-model"></a>Gegevensmodel bijwerken

Open _Models\Todo.cs_ in de code-editor. Voeg de volgende eigenschap toe aan de klasse `ToDo`:

```csharp
public bool Done { get; set; }
```

### <a name="run-code-first-migrations-locally"></a>Code First Migrations lokaal uitvoeren

Voer enkele opdrachten uit en werk de lokale database bij.

```bash
dotnet ef migrations add AddProperty
```

Werk de lokale database bij:

```bash
dotnet ef database update
```

### <a name="use-the-new-property"></a>Nieuwe eigenschap gebruiken

Breng enkele wijzigingen aan de code aan zodat de eigenschap `Done` kan worden gebruikt. Om deze zelfstudie eenvoudig te houden, wijzigt u eerst de weergaven `Index` en `Create` om de eigenschap in actie te zien.

Open _Controllers\TodosController.cs_.

Zoek de `Create()`-methode en voeg `Done` toe aan de lijst met eigenschappen in het attribuut `Bind`. Als u klaar bent, ziet uw `Create()`-methode er uit als de onderstaande code:

```csharp
public async Task<IActionResult> Create([Bind("ID,Description,CreatedDate,Done")] Todo todo)
```

Open _Views\Todos\Create.cshtml_.

In de Razor-code zou u een `<div class="form-group">`-element voor `Description` moeten zien en vervolgens een ander `<div class="form-group">`-element voor `CreatedDate`. Voeg direct na deze twee elementen een ander `<div class="form-group">`-element voor `Done` toe:

```csharp
<div class="form-group">
    <label asp-for="Done" class="col-md-2 control-label"></label>
    <div class="col-md-10">
        <input asp-for="Done" class="form-control" />
        <span asp-validation-for="Done" class="text-danger"></span>
    </div>
</div>
```

Open _Views\Todos\Index.cshtml_.

Zoek het lege `<th></th>`-element. Vlak boven dit element voegt u de volgende Razor-code toe:

```csharp
<th>
    @Html.DisplayNameFor(model => model.Done)
</th>
```

Zoek het `<td>`-element dat de `asp-action`-taghelpers bevat. Vlak boven dit element voegt u de volgende Razor-code toe:

```csharp
<td>
    @Html.DisplayFor(modelItem => item.CreatedDate)
</td>
```

Meer hebt u niet nodig om de wijzigingen in de weergaven `Index` en `Create` te zien.

### <a name="test-your-changes-locally"></a>De wijzigingen lokaal testen

Voer de app lokaal uit.

```bash
dotnet run
```

Ga in de browser naar `http://localhost:5000/`. U kunt nu een taakitem toevoegen en **Gereed** aanvinken. Het moet nu als een voltooid taakitem worden weergegeven op uw startpagina. In de weergave `Edit` wordt het veld `Done` niet getoond omdat u de weergave `Edit` niet hebt gewijzigd.

### <a name="publish-changes-to-azure"></a>Wijzigingen publiceren in Azure

```bash
git commit -am "added done field"
git push azure master
```

Zodra `git push` voltooid is, gaat u naar de Azure-web-app en probeert u de nieuwe functionaliteit uit.

![Azure-web-app na Code First Migration](./media/app-service-web-tutorial-dotnetcore-sqldb/this-one-is-done.png)

Alle bestaande taakitems worden nog steeds weergegeven. Als u de .NET Core-app opnieuw publiceert, blijven bestaande gegevens in SQL Database behouden. En met Entity Framework Core Migrations wordt alleen het gegevensschema gewijzigd. De bestaande gegevens blijven ongewijzigd.

## <a name="manage-your-azure-web-app"></a>Uw Azure-web-app beheren

Ga naar [Azure Portal](https://portal.azure.com) om de web-app te zien die u hebt gemaakt.

Klik vanuit het linkermenu op **App Services** en klik op de naam van uw Azure-web-app.

![Navigatie in de portal naar de Azure-web-app](./media/app-service-web-tutorial-dotnetcore-sqldb/access-portal.png)

In de portal wordt standaard de pagina **Overzicht** van de web-app getoond. Deze pagina geeft u een overzicht van hoe uw app presteert. Hier kunt u ook algemene beheertaken uitvoeren, zoals bladeren, stoppen, starten, opnieuw opstarten en verwijderen. De tabbladen aan de linkerkant van de pagina tonen de verschillende configuratiepagina's die u kunt openen.

![App Service-pagina in Azure Portal](./media/app-service-web-tutorial-dotnetcore-sqldb/web-app-blade.png)

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

<a name="next"></a>
## <a name="next-steps"></a>Volgende stappen

Wat u hebt geleerd:

> [!div class="checklist"]
> * Een SQL-database in Azure maken
> * Een .NET Core-app verbinden met SQL Database
> * De app implementeren in Azure
> * Het gegevensmodel bijwerken en de app opnieuw implementeren
> * Logboeken vanaf Azure naar uw terminal streamen
> * De app in Azure Portal beheren

Ga door naar de volgende zelfstudie om te leren hoe u een aangepaste DNS-naam aan uw web-app kunt toewijzen.

> [!div class="nextstepaction"]
> [Een bestaande aangepaste DNS-naam toewijzen aan Azure Web Apps](app-service-web-tutorial-custom-domain.md)