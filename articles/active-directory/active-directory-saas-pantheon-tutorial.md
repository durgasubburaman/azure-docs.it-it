---
title: 'Esercitazione: Integrazione di Azure Active Directory con Pantheon | Documentazione Microsoft'
description: Informazioni su come configurare l&quot;accesso Single Sign-On tra Azure Active Directory e Pantheon.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
editor: na
ms.assetid: d2c965d1-666f-44c2-b08f-b73163096374
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: jeedes
translationtype: Human Translation
ms.sourcegitcommit: 52a42d6705d0d2cfb86865027f8315411d7aece0
ms.openlocfilehash: b14872daab1bddf18d68b1f0fb23fc74c12078ed


---
# <a name="tutorial-azure-active-directory-integration-with-pantheon"></a>Esercitazione: integrazione di Azure Active Directory con Pantheon

Questa esercitazione descrive come integrare Pantheon con Azure Active Directory (Azure AD).

L'integrazione di Pantheon con Azure AD offre i vantaggi seguenti:

- È possibile controllare in Azure AD chi può accedere a Pantheon
- È possibile abilitare gli utenti per l'accesso automatico a Pantheon (Single Sign-On) con i propri account Azure AD
- È possibile gestire gli account da una posizione centrale: il portale di Azure classico

Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

Per configurare l'integrazione di Azure AD con Pantheon, sono necessari gli elementi seguenti:

- Sottoscrizione di Azure AD.
- Sottoscrizione di Pantheon abilitata per l'accesso Single Sign-On


>[!NOTE] 
>Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.


A questo scopo, è consigliabile seguire le indicazioni seguenti:

- Non usare l'ambiente di produzione, a meno che non sia necessario.
- Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).


## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.

Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:

1. Aggiunta di Pantheon dalla raccolta
2. Configurazione e test dell'accesso Single Sign-On di Azure AD


## <a name="adding-pantheon-from-the-gallery"></a>Aggiunta di Pantheon dalla raccolta
Per configurare l'integrazione di Pantheon in Azure AD, è necessario aggiungere Pantheon dalla raccolta al proprio elenco di app SaaS gestite.

**Per aggiungere Pantheon dalla raccolta, seguire questa procedura:**

1. Nel **portale di Azure classico**fare clic su **Active Directory**nel riquadro di spostamento sinistro.

    ![Active Directory][1]

2. Nell'elenco **Directory** selezionare la directory per la quale si desidera abilitare l'integrazione delle directory.

3. Per aprire la visualizzazione applicazioni, nella visualizzazione directory fare clic su **Applications** nel menu superiore.

    ![Applications][2]

4. Fare clic su **Add** nella parte inferiore della pagina.

    ![Applicazioni][3]

5. Nella finestra di dialogo **Come procedere** fare clic su **Aggiungere un'applicazione dalla raccolta**.

    ![Applicazioni][4]

6. Nella casella di ricerca digitare **Pantheon**.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_01.png)

7. Nel riquadro dei risultati selezionare **Pantheon** e quindi fare clic su **Completa** per aggiungere l'applicazione.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_02.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurazione e test dell'accesso Single Sign-On di Azure AD
In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Pantheon con un utente test di nome "Britta Simon".

Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere l'utente controparte di Pantheon che corrisponde a un utente di Azure AD. In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Pantheon.

La relazione di collegamento viene stabilita assegnando al valore di **nome utente** in Azure AD lo stesso valore di **Username** (Nome utente) in Pantheon.

Per configurare e testare l'accesso Single Sign-On di Azure AD con Pantheon, è necessario eseguire le operazioni fondamentali seguenti:

1. **[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'uso di questa funzionalità.
2. **[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.
3. **[Creazione di un utente test di Pantheon](#creating-a-pantheon-test-user)**: per avere una controparte di Britta Simon in Pantheon collegata alla relativa rappresentazione in Azure AD.
4. **[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.
5. **[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurazione dell'accesso Single Sign-On di Azure AD

In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale di Azure classico e viene configurato l'accesso Single Sign-On nell'applicazione Pantheon.


**Per configurare Single Sign-On di Azure AD con Pantheon, seguire questa procedura:**

L'applicazione Pantheon si aspetta un formato specifico per l'asserzione SAML ed è richiesta l'impostazione del valore dell'attributo NameIdentifier con l'indirizzo di posta elettronica dell'utente. Per impostazione predefinita, Azure AD usa UserPrincipalName per l'attributo NameIdentifier. Per la corretta integrazione è però necessario modificare questo valore in modo che corrisponda all'indirizzo di posta elettronica dell'utente.
L'integrazione funzionerà solo dopo aver completato correttamente il mapping.

![Configura accesso Single Sign-On](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_06.png)
    
1. Nella pagina di integrazione dell'applicazione **Pantheon** del portale di Azure classico fare clic su **Configura accesso Single Sign-On** per aprire la finestra di dialogo **Configura accesso Single Sign-On**.
     
    ![Configura accesso Single Sign-On][6] 

2. Nella pagina **Stabilire come si desidera che gli utenti accedano a Pantheon** selezionare **Single Sign-On di Microsoft Azure AD** e quindi fare clic su **Avanti**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_03.png) 

3. Nella pagina **Configurare le impostazioni dell'app** seguire questa procedura:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_04.png) 

    a. Nella casella di testo **Identificatore** digitare l'URN usando il modello seguente: `urn:auth0:pantheon:<orgname>-SSO`
    
    b. Nella casella di testo **URL di risposta** digitare l'URL usando il modello seguente: `https://pantheon.auth0.com/login/callback?connection=<orgname>-SSO` 

    c. click **Avanti**
 
4. Nella pagina **Configura accesso Single Sign-On in Pantheon** seguire questa procedura:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_05.png)

    a. Fare clic su **Scarica certificato**e quindi salvare il file nel computer.

    b. Fare clic su **Avanti**.


5. Per ottenere l'accesso Single Sign-On configurato per l'applicazione, contattare il [team di supporto tecnico di Pantheon](https://pantheon.io/docs/getting-support) e comunicare le informazioni seguenti:

    • **Certificato**

    • **URL servizio Single Sign-On**

    >[!NOTE] 
    >È inoltre necessario fornire le informazioni sui domini di posta elettronica e la data e ora in cui si vuole abilitare la connessione. Per informazioni più dettagliate, vedere [qui](https://pantheon.io/docs/sso-organizations/).

6. Nel portale classico selezionare la conferma della configurazione dell'accesso Single Sign-On e quindi fare clic su **Avanti**.
    
    ![Single Sign-On di Microsoft Azure AD][10]

7. Nella pagina **Conferma Single Sign-on** fare clic su **Completa**.  
 
    ![Single Sign-On di Microsoft Azure AD][11]


### <a name="creating-an-azure-ad-test-user"></a>Creazione di un utente test di Azure AD
In questa sezione viene creato un utente test chiamato Britta Simon nel portale classico.


![Creare un utente di Azure AD][20]

**Per creare un utente test in Azure AD, eseguire la procedura seguente:**

1. Nel **portale di Azure classico** fare clic su **Active Directory** nel riquadro di spostamento sinistro.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-pantheon-tutorial/create_aaduser_09.png) 

2. Nell'elenco **Directory** selezionare la directory per la quale si desidera abilitare l'integrazione delle directory.

3. Per visualizzare l'elenco di utenti, fare clic su **Utenti**nel menu in alto.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-pantheon-tutorial/create_aaduser_03.png) 

4. Per aprire la finestra di dialogo **Aggiungi utente**, fare clic su **Aggiungi utente** nella barra degli strumenti in basso.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-pantheon-tutorial/create_aaduser_04.png) 

5. Nella pagina **Informazioni sull'utente** seguire questa procedura:  ![Creazione di un utente test di Azure AD](./media/active-directory-saas-pantheon-tutorial/create_aaduser_05.png) 

    a. In Tipo di utente selezionare Nuovo utente nell'organizzazione.

    b. Nella casella di testo **Nome utente** digitare **BrittaSimon**.

    c. Fare clic su **Avanti**.

6.  Nella pagina **Profilo utente** seguire questa procedura: ![Creazione di un utente test di Azure AD](./media/active-directory-saas-pantheon-tutorial/create_aaduser_06.png) 

    a. Nella casella di testo **Nome** digitare **Britta**.  

    b. Nella casella di testo **Cognome** digitare **Simon**.

    c. Nella casella di testo **Nome visualizzato** digitare **Britta Simon**.

    d. Nell'elenco **Ruolo** selezionare **Utente**.

    e. Fare clic su **Avanti**.

7. Nella pagina **Ottieni password temporanea** fare clic su **crea**.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-pantheon-tutorial/create_aaduser_07.png) 

8. Nella pagina **Ottieni password temporanea** seguire questa procedura:

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-pantheon-tutorial/create_aaduser_08.png) 

    a. Prendere nota del valore visualizzato in **Nuova password**.

    b. Fare clic su **Completa**.   



### <a name="creating-an-pantheon-test-user"></a>Creazione di un utente di test di Pantheon

In questa sezione viene creato un utente di nome Britta Simon in Pantheon. Seguire i passaggi seguenti per aggiungere l'utente in Pantheon. 

>[!NOTE] 
>Per il corretto funzionamento di Single Sign-On è prima necessario creare l'utente in Pantheon.

1. Accedere a Pantheon con credenziali di amministratore.

2. Passare alla pagina del dashboard **Organization** (Organizzazione).
 
3. Fare clic su **Persone**.

4. Fare clic su **Add User**.

5. Immettere l'indirizzo di posta elettronica dell'utente.

6. Scegliere il ruolo dell'utente.

7. Fare clic su **Add User**.


### <a name="assigning-the-azure-ad-test-user"></a>Assegnazione dell'utente test di Azure AD

In questa sezione, Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Pantheon.

![Assegna utente][200] 

**Per assegnare Britta Simon a Pantheon, seguire questa procedura:**

1. Per aprire la visualizzazione delle applicazioni nel portale classico, nella visualizzazione directory fare clic su **Applicazioni** nel menu in alto.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni selezionare **Pantheon**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_50.png) 

3. Scegliere **Utenti**dal menu in alto.

    ![Assegna utente][203]

4. Nell'elenco di utenti selezionare **Britta Simon**.

5. Fare clic su **Assegna**sulla barra degli strumenti in basso.

    ![Assegna utente][205]


### <a name="testing-single-sign-on"></a>Test dell'accesso Single Sign-On

In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.

Quando si fa clic sul riquadro Pantheon nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione Pantheon.


## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_205.png



<!--HONumber=Dec16_HO1-->


