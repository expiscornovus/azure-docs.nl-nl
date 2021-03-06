---
title: 'Zelfstudie: Azure Active Directory-integratie met netwerken Palo Alto - Admin UI | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Palo Alto Networks - Admin UI.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: a826eaec-15af-4c85-8855-8a3374d1efb9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/01/2017
ms.author: jeedes
ms.openlocfilehash: 60430f08f54232db619efd054ca3a7d9a44f4cdc
ms.sourcegitcommit: 12fa5f8018d4f34077d5bab323ce7c919e51ce47
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 02/23/2018
---
# <a name="tutorial-azure-active-directory-integration-with-palo-alto-networks---admin-ui"></a>Zelfstudie: Azure Active Directory-integratie met netwerken Palo Alto - Admin UI

In deze zelfstudie leert u hoe integreren Palo Alto Networks - Admin UI met Azure Active Directory (Azure AD).

Netwerken Palo Alto - Admin UI met Azure AD integreren biedt de volgende voordelen:

- U kunt beheren in Azure AD die toegang hebben tot netwerken Palo Alto - Admin UI.
- U kunt uw gebruikers automatisch ophalen aangemeld bij Palo Alto Networks - Admin UI (Single Sign-On) met hun Azure AD-accounts kunt inschakelen.
- U kunt uw accounts op één centrale locatie - en de Azure-portal beheren.

Als u weten van meer informatie over de integratie van de SaaS-app met Azure AD wilt, Zie [wat is er toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Vereisten

Voor het configureren van Azure AD-integratie met netwerken Palo Alto - Admin UI, moet u de volgende items:

- Een Azure AD-abonnement
- Een Palo Alto netwerken Next Generation Firewall of Panorama (systeem voor de firewalls gecentraliseerd beheer)

> [!NOTE]
> Test de stappen in deze zelfstudie, raden we niet met behulp van een productieomgeving.

Test de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik niet uw productieomgeving, tenzij het noodzakelijk is.
- Als u geen een proefabonnement Azure AD-omgeving hebt, kunt u [ophalen van een proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u Azure AD eenmalige aanmelding in een testomgeving. Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Netwerken Palo Alto - Admin UI uit de galerie toevoegen
2. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-palo-alto-networks---admin-ui-from-the-gallery"></a>Netwerken Palo Alto - Admin UI uit de galerie toevoegen
Om de integratie van netwerken Palo Alto - Admin UI met Azure AD te configureren die u wilt toevoegen Palo Alto Networks - Admin UI uit de galerie aan de lijst met beheerde SaaS-apps.

**Als u wilt toevoegen, Palo Alto Networks - Admin UI uit de galerie, moet u de volgende stappen uitvoeren:**

1. In de  **[Azure-portal](https://portal.azure.com)**, klik in het linkernavigatievenster op **Azure Active Directory** pictogram. 

    ![De Azure Active Directory-knop][1]

2. Navigeer naar **bedrijfstoepassingen**. Ga vervolgens naar **alle toepassingen**.

    ![De blade Enterprise-toepassingen][2]
    
3. Om de nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.

    ![De knop Nieuw toepassing][3]

4. Typ in het zoekvak **Palo Alto Networks - Admin UI**, selecteer **Palo Alto Networks - Admin UI** van resultaat deelvenster klik vervolgens op **toevoegen** om toe te voegen van de toepassing.

    ![Netwerken Palo Alto - Admin UI in de lijst met resultaten](./media/active-directory-saas-paloaltoadmin-tutorial/tutorial_step4-add-from-the-gallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configureren en testen eenmalige aanmelding Azure AD

In deze sectie kunt u configureren en testen Azure AD eenmalige aanmelding met netwerken Palo Alto - Admin UI op basis van een testgebruiker 'Britta Simon' genoemd.

Voor eenmalige aanmelding werkt, moet Azure AD weten wat de gebruiker equivalent in Palo Alto Networks - Admin UI is aan een gebruiker in Azure AD. Met andere woorden, een koppeling relatie tussen een Azure AD-gebruiker en de betreffende gebruiker in netwerken Palo Alto - Admin UI moet tot stand worden gebracht.

In netwerken Palo Alto - Admin UI, wijs de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.

Als u wilt configureren en testen Azure AD eenmalige aanmelding met netwerken Palo Alto - Admin UI, moet u voor het voltooien van de volgende elementen:

1. **[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.
2. **[Maken van een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.
3. **[Maak een netwerken Palo Alto - Admin UI testgebruiker](#create-a-palo-alto-networks---admin-ui-test-user)**  - Palo Alto Networks - Admin UI die is gekoppeld aan de Azure AD-weergave van de gebruiker van een exemplaar van Britta Simon bevatten.
4. **[Toewijzen van de Azure AD-testgebruiker](#assign-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.
5. **[Test eenmalige aanmelding](#test-single-sign-on)**  : om te controleren of de configuratie werkt.

### <a name="configure-azure-ad-single-sign-on"></a>Eenmalige aanmelding Azure AD configureren

In dit gedeelte Azure AD eenmalige aanmelding inschakelen in de Azure portal en eenmalige aanmelding configureren in uw netwerken Palo Alto - Admin UI-toepassing.

**Voor het configureren van Azure AD eenmalige aanmelding met netwerken Palo Alto - Admin UI, moet u de volgende stappen uitvoeren:**

1. In de Azure-portal op de **Palo Alto Networks - Admin UI** toepassing Integratiepagina, klikt u op **eenmalige aanmelding**.

    ![Koppeling voor eenmalige aanmelding configureren][4]

2. Op de **eenmalige aanmelding** dialoogvenster Selecteer **modus** als **op basis van SAML aanmelding** voor eenmalige aanmelding inschakelen.
 
    ![Dialoogvenster voor eenmalige aanmelding](./media/active-directory-saas-paloaltoadmin-tutorial/tutorial_paloaltoadmin_samlbase.png)

3. Op de **Palo Alto Networks - domein voor beheer-UI en URL's** sectie, voert u de volgende stappen uit:

    ![Netwerken voor Palo Alto - domein voor beheer-UI en één URL's aanmelding informatie](./media/active-directory-saas-paloaltoadmin-tutorial/tutorial_general_show_advanced_url.png)
    
    a. In de **aanmeldings-URL** textbox, typ een URL met het volgende patroon volgen: `https://<Customer Firewall FQDN>/php/login.php`

    b. In de **id** textbox, typ een URL met het volgende patroon volgen: `https://<Customer Firewall FQDN>:443/SAML20/SP`
    
    c. In de **antwoord-URL** textbox Typ Assertion Consumer Service (ACS)-URL met het volgende patroon volgen: `https://<Customer Firewall FQDN>:443/SAML20/SP/ACS`
    

    > [!NOTE] 
    > Deze waarden zijn niet echt. Deze waarden bijwerken met het werkelijke aanmeldings-URL en de id. Neem contact op met [Palo Alto Networks - gebruikersinterface Beheerclient ondersteuningsteam](https://support.paloaltonetworks.com/support) ophalen van deze waarden. 
 
4. Netwerken Palo Alto - Admin UI toepassing verwacht de SAML-asserties in een specifieke indeling. Configureer de volgende claims voor deze toepassing. U kunt beheren de waarden van deze kenmerken van de '**gebruikerskenmerken**' sectie op de pagina van de toepassing-integratie. De volgende Schermafbeelding toont een voorbeeld voor deze.
    
    ![Eenmalige aanmelding configureren](./media/active-directory-saas-paloaltoadmin-tutorial/tutorial_paloaltoadmin_attribute.png)
    
5. In de **gebruikerskenmerken** sectie op de **eenmalige aanmelding** dialoogvenster SAML-token kenmerk configureren zoals wordt weergegeven in de afbeelding hierboven en voer de volgende stappen uit: kenmerkwaarden zijn alleen voorbeeld Neem de juiste waarden voor de gebruikersnaam en het adminrole worden toegewezen. Er is een andere optionele kenmerk 'accessdomain' die wordt gebruikt voor de beheerderstoegang beperken tot specifieke virtuele systemen op de firewall.
        
    | Naam kenmerk | Waarde kenmerk |
    | --- | --- |    
    | gebruikersnaam | user.userprincipalname |
    | adminrole | customadmin |

    a. Klik op **toevoegen kenmerk** openen de **kenmerk toevoegen** dialoogvenster.

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-paloaltoadmin-tutorial/tutorial_attribute_04.png)

    ![Eenmalige aanmelding configureren](./media/active-directory-saas-paloaltoadmin-tutorial/tutorial_attribute_05.png)
    
    b. In de **naam** textbox, typ de naam van het kenmerk wordt weergegeven voor die rij.
    
    c. Van de **waarde** typt u de waarde van het kenmerk wordt weergegeven voor die rij.
    
    d. Klik op **Ok**

    > [!NOTE]
    > U kunt verwijzen de volgende artikelen voor meer informatie over de kenmerken.
    > 1. Administratieve rol profiel voor Admin UI (adminrole): https://www.paloaltonetworks.com/documentation/80/pan-os/pan-os/firewall-administration/manage-firewall-administrators/configure-an-admin-role-profile
    > 2. Apparaat toegang domein voor Admin UI (accessdomain): https://www.paloaltonetworks.com/documentation/80/pan-os/web-interface-help/device/device-access-domain

6. Op de **SAML-certificaat voor ondertekening van** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.

    ![De downloadkoppeling certificaat](./media/active-directory-saas-paloaltoadmin-tutorial/tutorial_paloaltoadmin_certificate.png) 

7. Klik op **opslaan** knop.

    ![Knop Single Sign-On opslaan configureren](./media/active-directory-saas-paloaltoadmin-tutorial/tutorial_general_400.png)

8. Open de Palo Alto netwerken Firewall Admin gebruikersinterface als een beheerder in een ander browservenster.

9. Klik op **apparaat**.

    ![Eenmalige aanmelding Palo Alto configureren](./media/active-directory-saas-paloaltoadmin-tutorial/tutorial_paloaltoadmin_admin1.png)

10. Selecteer **SAML-identiteitsprovider** uit het linkernavigatiegedeelte staaf- en klik op 'Importeren' voor het importeren van het bestand met metagegevens.

    ![Eenmalige aanmelding Palo Alto configureren](./media/active-directory-saas-paloaltoadmin-tutorial/tutorial_paloaltoadmin_admin2.png)

11. Uitvoeren van volgende acties op het venster importeren

    ![Eenmalige aanmelding Palo Alto configureren](./media/active-directory-saas-paloaltoadmin-tutorial/tutorial_paloaltoadmin_idp.png)

    a. In de **profielnaam** textbox, Geef een naam bijvoorbeeld AzureAD Admin gebruikersinterface.
    
    b. In **identiteit Provider metagegevens**, klikt u op **Bladeren** en selecteer het metadata.xml-bestand dat u hebt gedownload vanuit Azure-portal
    
    c. Schakel '**valideren Provider identiteitscertificaat**'
    
    d. Klik op **OK**
    
    e. De configuraties van de firewall door te selecteren doorvoeren **doorvoeren** knop

12. Selecteer **SAML-identiteitsprovider** in de linkernavigatiebalk en klik op het profiel van een serviceprovider SAML identiteit (bijvoorbeeld AzureAD Admin UI) die in de vorige stap hebt gemaakt. 
    
  ![Palo Alto netwerken eenmalige aanmelding configureren](./media/active-directory-saas-paloaltoadmin-tutorial/tutorial_paloaltoadmin_idp_select.png)

13. De volgende acties uitvoeren op de **SAML identiteit Provider Server-profiel** venster

  ![Configureer Palo Alto netwerken één logboek-out](./media/active-directory-saas-paloaltoadmin-tutorial/tutorial_paloaltoadmin_slo.png)
  
  a. In de **identiteit Provieder SLO URL** textbox, verwijder de eerder geïmporteerd SLO-URL en voeg de volgende URL: `https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0`
  
  b. Klik op **OK**


14. Klik op de Palo Alto netwerken Firewall Admin UI, **apparaat** en selecteer **beheerdersrollen**

15. Klik op de **toevoegen** knop. Geef een naam voor de rol beheerder (bijvoorbeeld fwadmin) in het venster Admin rol profiel. Deze rol Admin-naam moet overeenkomen met de naam van het SAML-beheerdersrol-kenmerk verzonden door de identiteitsprovider. In stap 5 zijn de beheerdersrol naam en waarde gemaakt. 

  ![Beheerdersrol Palo Alto-netwerken configureren](./media/active-directory-saas-paloaltoadmin-tutorial/tutorial_paloaltoadmin_adminrole.png)
  
16. Klik op de Firewall Admin UI, **apparaat** en selecteer **Authentication profiel**

17. Klik op de **toevoegen** knop. In het venster Authentication profiel, moet u de volgende acties uitvoeren: 

 ![Palo Alto netwerken verificatie-profiel configureren](./media/active-directory-saas-paloaltoadmin-tutorial/tutorial_paloaltoadmin_authentication_profile.png)

   a. In de **naam** tekstvak een naam bijvoorbeeld AzureSAML_Admin_AuthProfile opgeven
    
   b. In **Type** vervolgkeuzelijst **SAML** 
   
   c. Selecteer het juiste SAML Identity Provider Server-profiel (bijvoorbeeld AzureAD Admin UI) in de vervolgkeuzelijst IdP Server-profiel
   
   c. Selecteer "**één afmelding inschakelen**' selectievakje
    
   d. Voer de naam van het kenmerk (bijvoorbeeld adminrole) in het tekstvak voor de beheerder Role-kenmerk. 
   
   e. Tabblad Geavanceerde selecteren en op **toevoegen** knop in het deelvenster lijst toestaan. Selecteer alle of specifieke gebruikers en groepen die kunnen worden geverifieerd met dit profiel. Wanneer een gebruiker zich verifieert, de firewall overeenkomt met de gekoppelde gebruikersnaam of de groep op basis van de vermeldingen in de lijst. Als u geen vermeldingen toevoegt, kunnen er zijn geen gebruikers verifiëren.
   
   ![Palo Alto netwerken verificatie-profiel configureren](./media/active-directory-saas-paloaltoadmin-tutorial/tutorial_paloaltoadmin_allowlist.png)
   
   f. Klik op **OK**

18. Als beheerders SAML SSO met behulp van Azure gebruiken, klikt u op **apparaat** en selecteer **Setup**. Selecteer in het deelvenster Setup **Management** tabblad en klik op het pictogram Tandwielpictogram onder **verificatie-instellingen**. 

 ![Palo Alto netwerken verificatie-instellingen configureren](./media/active-directory-saas-paloaltoadmin-tutorial/tutorial_paloaltoadmin_authsetup.png)

19. Selecteer het profiel SAML-verificatie is gemaakt in stap 17. (bijvoorbeeld AzureSAML_Admin_AuthProfile)

 ![Palo Alto netwerken verificatie-instellingen configureren](./media/active-directory-saas-paloaltoadmin-tutorial/tutorial_paloaltoadmin_authsettings.png)

20. Klik op **OK**

21. Voer de configuratie door te selecteren **doorvoeren** knop.


> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl u de app instelt!  Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de **configuratie** sectie onderaan. U kunt meer lezen over de ingesloten documentatie-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Een Azure AD-testgebruiker maken

Het doel van deze sectie is het een testgebruiker maken in de Azure portal Britta Simon aangeroepen.

   ![Een Azure AD-testgebruiker maken][100]

**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**

1. Klik in de Azure-portal in het linkerdeelvenster op het **Azure Active Directory** knop.

    ![De Azure Active Directory-knop](./media/active-directory-saas-paloaltoadmin-tutorial/create_aaduser_01.png)

2. Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.

    !['Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/active-directory-saas-paloaltoadmin-tutorial/create_aaduser_02.png)

3. Openen van de **gebruiker** in het dialoogvenster klikt u op **toevoegen** boven aan de **alle gebruikers** in het dialoogvenster.

    ![De knop toevoegen](./media/active-directory-saas-paloaltoadmin-tutorial/create_aaduser_03.png)

4. In de **gebruiker** dialoogvenster vak, voert u de volgende stappen uit:

    ![Het dialoogvenster gebruiker](./media/active-directory-saas-paloaltoadmin-tutorial/create_aaduser_04.png)

    a. In de **naam** in het vak **BrittaSimon**.

    b. In de **gebruikersnaam** typt u het e-mailadres van gebruiker Britta Simon.

    c. Selecteer de **wachtwoord weergeven** selectievakje, en noteer de waarde die wordt weergegeven in de **wachtwoord** vak.

    d. Klik op **Create**.
 
### <a name="create-a-palo-alto-networks---admin-ui-test-user"></a>Een netwerken Palo Alto - Admin UI testgebruiker maken

Netwerken Palo Alto - Admin UI ondersteunt Just-in-time gebruikersaanvragen zodat een gebruiker automatisch in het systeem na een geslaagde authenticatie gemaakt wordt als dat niet al bestaat. U hoeft niet hier actie uit te voeren.

### <a name="assign-the-azure-ad-test-user"></a>De Azure AD-testgebruiker toewijzen

In deze sectie schakelt u Britta Simon Azure eenmalige aanmelding gebruiken door het verlenen van toegang tot netwerken Palo Alto - Admin UI.

![Toewijzen van de gebruikersrol][200] 

**Britta Simon om aan te wijzen Palo Alto Networks - Admin UI, moet u de volgende stappen uitvoeren:**

1. Open de weergave toepassingen in de Azure-portal en gaat u naar de directoryweergave en gaat u naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

2. Selecteer in de lijst met toepassingen **Palo Alto Networks - Admin UI**.

    ![De netwerken Palo Alto - Admin UI-koppeling in de lijst met toepassingen](./media/active-directory-saas-paloaltoadmin-tutorial/tutorial_paloaltoadmin_app.png)  

3. Klik in het menu aan de linkerkant op **gebruikers en groepen**.

    ![De koppeling 'Gebruikers en groepen'][202]

4. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Het deelvenster toewijzing toevoegen][203]

5. Op **gebruikers en groepen** dialoogvenster Selecteer **Britta Simon** in de lijst gebruikers.

6. Klik op **Selecteer** knop op **gebruikers en groepen** dialoogvenster.

7. Klik op **toewijzen** knop op **toevoegen toewijzing** dialoogvenster.
    
### <a name="test-single-sign-on"></a>Test eenmalige aanmelding

In deze sectie kunt u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster testen.

Wanneer u klikt op de netwerken Palo Alto - Admin UI-tegel in het deelvenster toegang u moet ophalen automatisch aangemeld bij uw netwerken Palo Alto - Admin UI-toepassing.
Zie voor meer informatie over het toegangsvenster [Inleiding tot het toegangsvenster](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Aanvullende resources

* [Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Wat is de toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-paloaltoadmin-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-paloaltoadmin-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-paloaltoadmin-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-paloaltoadmin-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-paloaltoadmin-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-paloaltoadmin-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-paloaltoadmin-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-paloaltoadmin-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-paloaltoadmin-tutorial/tutorial_general_203.png

