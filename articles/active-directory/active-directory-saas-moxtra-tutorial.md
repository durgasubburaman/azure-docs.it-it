---
title: 'Esercitazione: integrazione di Azure Active Directory con Moxtra | Documentazione Microsoft'
description: Informazioni su come configurare l&quot;accesso Single Sign-On tra Azure Active Directory e Moxtra.
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 2aed2d4b-1dcd-4839-8fed-9419d107c61c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/23/2017
ms.author: jeedes
translationtype: Human Translation
ms.sourcegitcommit: 4a07f946d396a9263d5b00202cd5229ddc86d1be
ms.openlocfilehash: cbb93424c6315ec7605bb238fd40dc62ccbb4e17
ms.lasthandoff: 03/01/2017


---
# <a name="tutorial-azure-active-directory-integration-with-moxtra"></a>Esercitazione: integrazione di Azure Active Directory con Moxtra
Questa esercitazione descrive l'integrazione di Moxtra con Azure Active Directory (Azure AD).

L'integrazione di Moxtra con Azure AD offre i vantaggi seguenti: 

* È possibile controllare in Azure AD chi può accedere a Moxtra 
* È possibile abilitare gli utenti per l'accesso Single Sign-On automatico a Moxtra (SSO) con i propri account Azure AD
* È possibile gestire gli account da una posizione centrale: il portale di Azure classico

Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti
Per configurare l'integrazione di Azure AD con Moxtra, sono necessari gli elementi seguenti:

* Sottoscrizione di Azure AD.
* Sottoscrizione Moxtra abilitata per l'accesso Single Sign-On (SSO)

>[!NOTE]
>Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione. 
> 

A questo scopo, è consigliabile seguire le indicazioni seguenti:

* Non usare l'ambiente di produzione, a meno che non sia necessario.
* Se non è disponibile un ambiente di prova di Azure AD, è possibile ottenere una versione di prova di un mese [qui](https://azure.microsoft.com/pricing/free-trial/). 

## <a name="scenario-description"></a>Descrizione dello scenario
L'obiettivo di questa esercitazione è testare l'accesso Single Sign-On di Azure AD in un ambiente di test. 

Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:

1. Aggiunta di Moxtra dalla raccolta 
2. Configurazione e test dell'accesso Single Sign-On (SSO) di Microsoft Azure AD

## <a name="adding-moxtra-from-the-gallery"></a>Aggiunta di Moxtra dalla raccolta
Per configurare l'integrazione di Moxtra in Azure AD, è necessario aggiungere Moxtra dalla raccolta al proprio elenco di app SaaS gestite.

**Per aggiungere Moxtra dalla raccolta, seguire questa procedura:**

1. Nel **portale di Azure classico**fare clic su **Active Directory**nel riquadro di spostamento sinistro. 
   
    ![Active Directory][1]
2. Nell'elenco **Directory** selezionare la directory per la quale si desidera abilitare l'integrazione delle directory.
3. Per aprire la visualizzazione applicazioni, nella visualizzazione directory fare clic su **Applications** nel menu superiore.
   
    ![Applications][2]
4. Fare clic su **Add** nella parte inferiore della pagina.
   
    ![Applicazioni][3]
5. Nella finestra di dialogo **Come procedere** fare clic su **Aggiungere un'applicazione dalla raccolta**.
   
    ![Applicazioni][4]
6. Nella casella di ricerca, digitare **Moxtra**.
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_01.png)
7. Nel riquadro dei risultati, selezionare **Moxtra**, quindi fare clic su **Completa** per aggiungere l'applicazione.
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_02.png)

## <a name="configuring-and-testing-azure-ad-sso"></a>Configurazione e test dell'accesso Single Sign-On (SSO) di Microsoft Azure AD
Questa sezione descrive come configurare e testare l'accesso SSO di Azure AD con Moxtra con un utente test di nome "Britta Simon".

Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di Moxtra che corrisponde a un utente di Azure AD. In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Moxtra.

La relazione di collegamento viene stabilita assegnando al valore di **nome utente** in Azure AD lo stesso valore di **Nome utente** in Moxtra.

Per configurare e testare l'accesso Single Sign-On di Azure AD con Moxtra, è necessario completare i blocchi predefiniti seguenti:

1. **[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-single-sign-on)**: per abilitare gli utenti all'uso di questa funzionalità.
2. **[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.
3. **[Creare un utente test Moxtra](#creating-a-moxtra-test-user)** - per avere una controparte di Britta Simon in Moxtra collegata alla relativa rappresentazione in Azure AD.
4. **[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.
5. **[Test dell'accesso Single Sign-On](#testing-single-sign-on)**: per verificare se la configurazione funziona.

### <a name="configure-azure-ad-sso"></a>Configurare l'accesso SSO di Azure AD
Questa sezione descrive come abilitare l'accesso Single Sign-On di Azure AD nel portale di Azure classico e configurare l'accesso SSO nell'applicazione Moxtra. 

L'applicazione Moxtra prevede un formato specifico per le asserzioni SAML. È quindi necessario aggiungere mapping di attributi personalizzati alla configurazione degli attributi del token SAML. La schermata seguente illustra un esempio relativo a questa operazione.

![Configura accesso Single Sign-On](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_09.png) 

**Per configurare l'accesso Single Sign-On di Azure AD con Moxtra, seguire questa procedura:**

1. Nella pagina di integrazione dell'applicazione **Moxtra** del portale di Azure classico, fare clic su **Configura accesso Single Sign-On** per aprire la finestra di dialogo **Configura accesso Single Sign-On**.
   
    ![Configura accesso Single Sign-On][6] 
2. Nella pagina **Stabilire come si desidera che gli utenti accedano a Moxtra** selezionare **Single Sign-On di Azure AD** e quindi fare clic su **Avanti**.
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_03.png) 
3. Nella pagina **Configurare le impostazioni dell'app** seguire questa procedura:
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_04.png) 
  1. Nella casella di testo **URL di accesso** digitare l'URL seguente: **https://www.moxtra.com/service/#login**. 
  2. Fare clic su **Avanti**.
4. Nella pagina **Configura accesso Single Sign-On in Moxtra** seguire questa procedura:
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_05.png) 
  1. Fare clic su **Scarica certificato**e quindi salvare il file nel computer.
  2. Fare clic su **Avanti**.
5. In un'altra finestra del browser, accedere al sito aziendale di Moxtra come amministratore.
6. Nella barra degli strumenti a sinistra, fare clic su**Admin Console > SAML Single Sign-On**, quindi su **Nuovo**.
   
  ![Configura accesso Single Sign-On](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_06.png) 
7. Nella pagina **SAML** , eseguire i passaggi seguenti:
   
  ![Configura accesso Single Sign-On](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_08.png)   
  1. Nella casella di testo **Nome** , digitare un nome per la configurazione (ad esempio *SAML*). 
  2. Nella pagina della finestra di dialogo **Configura accesso Single Sign-On in Moxtra** del portale di Azure classico copiare il valore di **ID entità** e incollarlo nella casella di testo **IdP Entity ID**. 
  3. Nella pagina della finestra di dialogo **Configura accesso Single Sign-On in Moxtra** del portale di Azure classico, copiare il valore di **URL di accesso remoto** e incollarlo nella casella di testo **URL di accesso**. 
  4. Nella casella di testo **AuthnContextClassRef** digitare **urn:oasis:names:tc:SAML:2.0:ac:classes:Password**. 
  5. Nella pagina della finestra di dialogo **Configura accesso Single Sign-On in Moxtra** nel portale di Azure classico, copiare il valore di **Formato identificatore nome** e quindi incollarlo nella casella di testo **Format ID nome**. 
  6. Aprire il certificato scaricato nel Blocco note, copiarne il contenuto e incollarlo nella casella di testo **Certificato** .    
  7. Nella casella di testo dominio email SAML, digitare il dominio email SAML.    
   
   >[!NOTE]
   >Per verificare il dominio, fare clic su “**i**” di seguito.
   >  
  8. Fare clic su **Update**.
8. Nel portale di Azure classico selezionare la conferma della configurazione dell'accesso Single Sign-On e fare clic su **Avanti**. 
   
  ![Single Sign-On di Microsoft Azure AD][10]
9. Nella pagina **Conferma Single Sign-on** fare clic su **Completa**.  
  
  ![Single Sign-On di Microsoft Azure AD][11]
19. Per aggiungere il mapping degli attributi personalizzato alla configurazione degli attributi token SAML, nel menu in alto fare clic su **Attributi** per aprire la finestra di dialogo **Attributi del token SAML**. 
   
  ![Configura accesso Single Sign-On](./media/active-directory-saas-moxtra-tutorial/tutorial_general_80.png) 
11. Per ogni riga di dati nella tabella precedente, seguire questa procedura:
   
     | Nome attributo | Valore attributo |
     | --- | --- |
     | firstname |givenname |
     | lastname |surname |
     | idpid |*\<il valore di **ID entità** dalla pagina **Configura accesso Single Sign-On in Moxtra** nel portale di Azure classico\>* |
  1. Fare clic su Aggiungi attributo utente. 

     ![Configura accesso Single Sign-On](./media/active-directory-saas-moxtra-tutorial/tutorial_general_81.png) 
  2. Nella pagina **Aggiungi attributo utente** , digitare il nome e il valore dell’attributo mostrati per quella riga nella tabella. 

     ![Configura accesso Single Sign-On](./media/active-directory-saas-moxtra-tutorial/tutorial_general_82.png) 
  3. Fare clic su **Completa**.
12. Fare clic su **Applica modifiche**. 
   
  ![Configura accesso Single Sign-On](./media/active-directory-saas-moxtra-tutorial/tutorial_general_84.png) 

### <a name="create-an-azure-ad-test-user"></a>Creare un utente test di Azure AD
Questa sezione descrive come creare un utente test chiamato Britta Simon nel portale di Azure classico.  

![Creare un utente di Azure AD][20]

**Per creare un utente test in Azure AD, eseguire la procedura seguente:**

1. Nel **portale di Azure classico** fare clic su **Active Directory** nel riquadro di spostamento sinistro.
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-moxtra-tutorial/create_aaduser_09.png)  
2. Nell'elenco **Directory** selezionare la directory per la quale si desidera abilitare l'integrazione delle directory.
3. Per visualizzare l'elenco di utenti, fare clic su **Utenti**nel menu in alto.
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-moxtra-tutorial/create_aaduser_03.png) 
4. Per aprire la finestra di dialogo **Aggiungi utente**, fare clic su **Aggiungi utente** nella barra degli strumenti in basso. 
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-moxtra-tutorial/create_aaduser_04.png) 
5. Nella pagina **Informazioni sull'utente** seguire questa procedura: 
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-moxtra-tutorial/create_aaduser_05.png)  
  1. In Tipo di utente selezionare Nuovo utente nell'organizzazione.
  2. Nella casella di testo **Nome utente** digitare **BrittaSimon**.
  3. Fare clic su **Avanti**.
6. Nella pagina **Profilo utente** seguire questa procedura: 
   
   ![Creazione di un utente test di Azure AD](./media/active-directory-saas-moxtra-tutorial/create_aaduser_06.png) 
  1. Nella casella di testo **Nome** digitare **Britta**.  
  2. Nella casella di testo **Cognome** digitare **Simon**.
  3. Nella casella di testo **Nome visualizzato** digitare **Britta Simon**.
  4. Nell'elenco **Ruolo** selezionare **Utente**.
  5. Fare clic su **Avanti**.
7. Nella pagina **Ottieni password temporanea** fare clic su **crea**.
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-moxtra-tutorial/create_aaduser_07.png) 
8. Nella pagina **Ottieni password temporanea** seguire questa procedura:
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-moxtra-tutorial/create_aaduser_08.png) 
  1. Prendere nota del valore visualizzato in **Nuova password**.
  2. Fare clic su **Complete**.   

### <a name="create-a-moxtra-test-user"></a>Creare un utente test Moxtra
Questa sezione descrive come creare un utente chiamato Britta Simon in Moxtra.

**Per creare un utente denominato Britta Simon in Moxtra, seguire questa procedura:**

1. Accedere al sito aziendale di Moxtra come amministratore.
2. Nella barra degli strumenti a sinistra, fare clic su**Admin Console > Gestione utente** e quindi su **Aggiungi utente**.
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_10.png) 
3. Nella finestra di dialogo **Aggiungi utente** seguire questa procedura:
  1. Nella casella di testo **Nome** digitare **Britta**.
  2. Nella casella di testo **Cognome** digitare **Simon**.
  3. Nella casella di testo **Posta elettronica** digitare l'indirizzo di posta elettronica di Britta Simon nel portale di Azure classico.
  4. Nella casella di testo **Divisione**, digitare **Dev**.
  5. Nella casella di testo **Reparto**, digitare **IT**.
  6. Selezionare **Amministratore**.
  7. Fare clic su **Aggiungi**.

### <a name="assign-the-azure-ad-test-user"></a>Assegnare l'utente test di Azure AD
Questa sezione descrive come abilitare Britta Simon a usare l'accesso Single Sign-On di Azure concedendole l'accesso a Moxtra.

![Assegna utente][200] 

**Per assegnare Britta Simon a Moxtra, seguire questa procedura:**

1. Per aprire la visualizzazione applicazioni nel portale di Azure classico, nella visualizzazione directory scegliere **Applicazioni** dal menu in alto.
   
    ![Assegna utente][201] 
2. Nell'elenco di applicazioni, selezionare **Moxtra**.
   
    ![Configura accesso Single Sign-On](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_50.png) 
3. Scegliere **Utenti**dal menu in alto.
   
    ![Assegna utente][203] 
4. Nell'elenco di utenti selezionare **Britta Simon**.
5. Fare clic su **Assegna**sulla barra degli strumenti in basso.
   
    ![Assegna utente][205]

### <a name="test-single-sign-on"></a>Testare l'accesso Single Sign-On
Questa sezione descrive come testare la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.  

Quando si fa clic sul riquadro Moxtra nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione Moxtra.

## <a name="additional-resources"></a>Risorse aggiuntive
* [Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_205.png







