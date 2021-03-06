---
title: 'Esercitazione: Integrazione di Azure Active Directory con 23 Video | Microsoft Docs'
description: Informazioni su come configurare l&quot;accesso Single Sign-On tra Azure Active Directory e 23 Video.
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 5e73dd1d-3995-4a73-b9cf-1b2318d49cb3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/24/2017
ms.author: jeedes
translationtype: Human Translation
ms.sourcegitcommit: a59a0782176f5221bb8b2f590faeee660f4d1101
ms.openlocfilehash: 2ebc4571cb7ff763449f192f5140c79a65d69833
ms.lasthandoff: 03/01/2017


---
# <a name="tutorial-azure-active-directory-integration-with-23-video"></a>Esercitazione: Integrazione di Azure Active Directory con 23 Video
Questa esercitazione descrive l’integrazione di 23 Video con Azure Active Directory (Azure AD).

L'integrazione di 23 Video con Azure AD offre i vantaggi seguenti: 

* È possibile controllare in Azure AD chi può accedere a 23 Video 
* È possibile abilitare gli utenti per l'accesso automatico Single Sign-On (SSO) a 23 Video con i propri account Azure AD

Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti
Per configurare l'integrazione di Azure AD con 23 Video, sono necessari gli elementi seguenti:

* Sottoscrizione di Azure AD.
* Sottoscrizione di 23 Video abilitata per l'accesso Single Sign-On (SSO)

>[!NOTE]
>Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione. 
> 

A questo scopo, è consigliabile seguire le indicazioni seguenti:

* Non usare l'ambiente di produzione, a meno che non sia necessario.
* Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/). 

## <a name="scenario-description"></a>Descrizione dello scenario
L'obiettivo di questa esercitazione è quello di testare l'accesso Single Sign-On (SSO) di Azure AD in un ambiente di test.

Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:

1. Aggiunta di 23 Video dalla raccolta 
2. Configurazione e test dell'accesso Single Sign-On (SSO) di Microsoft Azure AD

## <a name="adding-23-video-from-the-gallery"></a>Aggiunta di 23 Video dalla raccolta
Per configurare l'integrazione di 23 Video in Azure AD, è necessario aggiungere 23 Video dalla raccolta al proprio elenco di app SaaS gestite.

**Per aggiungere 23 Video dalla raccolta, seguire questa procedura:**

1. Nel **portale di Azure classico**fare clic su **Active Directory**nel riquadro di spostamento sinistro. 
   
    ![Active Directory][1]
2. Nell'elenco **Directory** selezionare la directory per la quale si desidera abilitare l'integrazione delle directory.
3. Per aprire la visualizzazione applicazioni, nella visualizzazione directory fare clic su **Applications** nel menu superiore.
   
    ![Applications][2]
4. Fare clic su **Add** nella parte inferiore della pagina.
   
    ![Applicazioni][3]
5. Nella finestra di dialogo **Come procedere** fare clic su **Aggiungere un'applicazione dalla raccolta**.
   
    ![Applicazioni][4]
6. Nella casella di ricerca digitare **23 Video**.
   
    ![Applicazioni][5]
7. Nel riquadro dei risultati selezionare **23 Video**, quindi fare clic su **Completa** per aggiungere l'applicazione.
   
    ![Applicazioni][25]

## <a name="configuring-and-testing-azure-ad-sso"></a>Configurazione e test dell'accesso Single Sign-On (SSO) di Microsoft Azure AD
Questa sezione descrive come configurare e testare l'accesso SSO di Azure AD con 23 Videos in base a un utente test di nome "Britta Simon".

Per il funzionamento dell'accesso SSO, Azure AD deve conoscere qual è l'utente di 23 Video che corrisponde a un utente di Azure AD. In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in 23 Video.  

La relazione di collegamento viene stabilita assegnando al valore di **nome utente** in Azure AD lo stesso valore di **Username** (Nome utente) in 23 Video.

Per configurare e testare l'accesso SSO di Azure AD con 23 Video, è necessario completare i blocchi predefiniti seguenti:

1. **[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-single-sign-on)**: per abilitare gli utenti all'uso di questa funzionalità.
2. **[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.
3. **[Creazione di un utente test per 23 Video](#creating-a-23-video-test-user)** : per avere una controparte di Britta Simon in 23 Video collegata alla relativa rappresentazione in Azure AD.
4. **[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.
5. **[Test dell'accesso Single Sign-On](#testing-single-sign-on)**: per verificare se la configurazione funziona.

### <a name="configure-azure-ad-sso"></a>Configurare l'accesso SSO di Azure AD
Questa sezione descrive come abilitare l'accesso Single Sign-On di Azure AD nel portale di Azure classico e configurare l'accesso SSO nell'applicazione 23 Video.

**Per configurare l'accesso SSO di Azure AD con 23 Video, seguire questa procedura:**

1. Nella pagina di integrazione dell'applicazione **23 Video** del portale di Azure classico fare clic su **Configura accesso Single Sign-On** per aprire la finestra di dialogo **Configura accesso Single Sign-On**.
   
    ![Configura accesso Single Sign-On][6] 
2. Nella pagina **Stabilire come si desidera che gli utenti accedano a 23 Video** selezionare **Single Sign-On di Azure AD** e quindi fare clic su **Avanti**.
   
    ![Single Sign-On di Microsoft Azure AD][7] 
3. Nella pagina **Configurare le impostazioni dell'app** seguire questa procedura:
   
    ![Single Sign-On di Microsoft Azure AD][8] 
  1. Nella casella di testo **URL di risposta** digitare l'URL usato dagli utenti per accedere al sito 23 Video, ad esempio *https://britta-simon.23Video.com/saml/login*.
   
    >[!NOTE]
    >L'integrazione di Active Directory tramite SAML 2.0 è disponibile per tutti gli utenti di 23 Video. Per ottenere i metadati corrispondenti, contattare il supporto tecnico all'indirizzo [support@23company.com](mailto:support@23company.com) . 
    > 
 
  2. Fare clic su **Avanti**.
4. Nella pagina **Configura accesso Single Sign-On in 23 Video** seguire questa procedura:
   
    ![Single Sign-On di Microsoft Azure AD][9] 
 1. Fare clic su Download certificato e quindi salvare il file nel computer.
 2. Contattare il team di supporto di 23 Video inviando un messaggio all'indirizzo [support@23company.com](mailto:support@23company.com), fornire il certificato scaricato e le informazioni visualizzate nei campi **URL autorità di certificazione**, **URL servizio Single Sign-On**, **URL servizio Single Sign-Out** e quindi chiedere di configurare l'accesso Single Sign-On per l'app 23 Video.    
 3. Fare clic su **Avanti**.
5. Nel portale di Azure classico selezionare la conferma della configurazione dell'accesso Single Sign-On e quindi fare clic su **Avanti**. 
   
    ![Single Sign-On di Microsoft Azure AD][10]
6. Nella pagina **Conferma Single Sign-on** fare clic su **Completa**.  
   
    ![Single Sign-On di Microsoft Azure AD][11]

### <a name="create-an-azure-ad-test-user"></a>Creare un utente test di Azure AD
Questa sezione descrive come creare un utente test chiamato Britta Simon nel portale di Azure classico.

![Creare un utente di Azure AD][20]

**Per creare un utente test in Azure AD, eseguire la procedura seguente:**

1. Nel **portale di Azure classico** fare clic su **Active Directory** nel riquadro di spostamento sinistro.
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-23video-tutorial/create_aaduser_09.png)  
2. Nell'elenco **Directory** selezionare la directory per la quale si desidera abilitare l'integrazione delle directory.
3. Per visualizzare l'elenco di utenti, fare clic su **Utenti**nel menu in alto.
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-23video-tutorial/create_aaduser_03.png) 
4. Per aprire la finestra di dialogo **Aggiungi utente**, fare clic su **Aggiungi utente** nella barra degli strumenti in basso. 
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-23video-tutorial/create_aaduser_04.png) 
5. Nella pagina **Informazioni sull'utente** seguire questa procedura: 
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-23video-tutorial/create_aaduser_05.png)  
 1. In Tipo di utente selezionare Nuovo utente nell'organizzazione. 
 2. Nella casella di testo **Nome utente** digitare **BrittaSimon**. 
 3. Fare clic su **Avanti**.
6. Nella pagina **Profilo utente** seguire questa procedura: 
   
   ![Creazione di un utente test di Azure AD](./media/active-directory-saas-23video-tutorial/create_aaduser_06.png)  
 1. Nella casella di testo **Nome** digitare **Britta**.   
 2. Nella casella di testo **Cognome** digitare **Simon**. 
 3. Nella casella di testo **Nome visualizzato** digitare **Britta Simon**. 
 4. Nell'elenco **Ruolo** selezionare **Utente**.
 5. Fare clic su **Avanti**.
7. Nella pagina **Ottieni password temporanea** fare clic su **crea**.
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-23video-tutorial/create_aaduser_07.png) 
8. Nella pagina **Ottieni password temporanea** seguire questa procedura:
   
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-23video-tutorial/create_aaduser_08.png)  
 1. Prendere nota del valore visualizzato in **Nuova password**. 
 2. Fare clic su **Complete**.   

### <a name="create-a-23-video-test-user"></a>Creare un utente test per 23 Video
Questa sezione descrive come creare un utente chiamato Britta Simon in 23 Video.

**Per creare un utente denominato Britta Simon in 23 Video, seguire questa procedura:**

1. Accedere al sito aziendale di 23 Video come amministratore.
2. Passare a **Impostazioni**.
3. Nella sezione **Users** (Utenti) fare clic su **Configure** (Configura).
   
    ![Assegna utente][400]
4. Fare clic su **Aggiungi nuovo utente**. 
   
    ![Assegna utente][401]
5. Nella sezione **Invita qualcuno a questo sito** seguire questa procedura:
   
    ![Assegna utente][402]
 1. Nella casella di testo **E-mail addresses** digitare l'indirizzo di posta elettronica di Britta Simon in Azure Active Directory.  
 2. Fare clic su **Aggiungi questo utente**.   

### <a name="assign-the-azure-ad-test-user"></a>Assegnare l'utente test di Azure AD
Questa sezione descrive come abilitare Britta Simon all'uso dell'accesso SSO di Azure concedendole l'accesso a 23 Video.

![Assegna utente][200] 

**Per assegnare Britta Simon a 23 Video, seguire questa procedura:**

1. Per aprire la visualizzazione applicazioni nel portale di Azure classico, nella visualizzazione directory fare clic su **Applicazioni** nel menu in alto.
   
    ![Assegna utente][201] 
2. Nell'elenco delle applicazioni selezionare **23 Video**.
   
    ![Assegna utente][202] 
3. Scegliere **Utenti**dal menu in alto.
   
    ![Assegna utente][203] 
4. Nell'elenco di utenti selezionare **Britta Simon**.
5. Fare clic su **Assegna**sulla barra degli strumenti in basso.
   
    ![Assegna utente][205]

### <a name="test-single-sign-on"></a>Testare l'accesso Single Sign-On
Questa sezione descrive come testare la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.

Quando si fa clic sul riquadro 23 Video nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione 23 Video.

## <a name="additional-resources"></a>Risorse aggiuntive
* [Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)

<!--Image references-->
[1]: ./media/active-directory-saas-23video-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-23video-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-23video-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-23video-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-23video-tutorial/tutorial_23video_01.png
[25]: ./media/active-directory-saas-23video-tutorial/tutorial_23video_02.png

[6]: ./media/active-directory-saas-23video-tutorial/tutorial_general_05.png
[7]: ./media/active-directory-saas-23video-tutorial/tutorial_23video_03.png
[8]: ./media/active-directory-saas-23video-tutorial/tutorial_23video_04.png
[9]: ./media/active-directory-saas-23video-tutorial/tutorial_23video_05.png
[10]: ./media/active-directory-saas-23video-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-23video-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-23video-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-23video-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-23video-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-23video-tutorial/tutorial_23video_07.png
[203]: ./media/active-directory-saas-23video-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-23video-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-23video-tutorial/tutorial_general_205.png

[400]: ./media/active-directory-saas-23video-tutorial/tutorial_23video_10.png
[401]: ./media/active-directory-saas-23video-tutorial/tutorial_23video_11.png
[402]: ./media/active-directory-saas-23video-tutorial/tutorial_23video_12.png





