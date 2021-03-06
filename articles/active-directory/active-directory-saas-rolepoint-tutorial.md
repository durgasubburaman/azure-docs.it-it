---
title: 'Esercitazione: Integrazione di Azure Active Directory con RolePoint | Documentazione Microsoft'
description: Informazioni su come configurare l&quot;accesso Single Sign-On tra Azure Active Directory e RolePoint.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 68d37f40-15da-45f5-a9e1-d53f78e786d1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/10/2017
ms.author: jeedes
translationtype: Human Translation
ms.sourcegitcommit: 07635b0eb4650f0c30898ea1600697dacb33477c
ms.openlocfilehash: ea9ddb361d013e58d55401112c98a72b487d92d3
ms.lasthandoff: 03/28/2017


---
# <a name="tutorial-azure-active-directory-integration-with-rolepoint"></a>Esercitazione: Integrazione di Azure Active Directory con RolePoint

Questa esercitazione descrive come integrare RolePoint con Azure Active Directory (Azure AD).

L'integrazione di RolePoint con Azure AD offre i vantaggi seguenti:

- È possibile controllare in Azure AD chi può accedere a RolePoint
- È possibile abilitare gli utenti per l'accesso automatico a RolePoint Single Sign-On (SSO) con i propri account Azure AD
- È possibile gestire gli account da una posizione centrale: il portale di Azure classico

Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

Per configurare l'integrazione di Azure AD con RolePoint, sono necessari gli elementi seguenti:

- Sottoscrizione di Azure AD.
- Sottoscrizione di RolePoint abilitata per l'accesso SSO

>[!NOTE]
>Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.
>

A questo scopo, è consigliabile seguire le indicazioni seguenti:

- Non usare l'ambiente di produzione, a meno che non sia necessario.
- Se non è disponibile un ambiente di valutazione di Azure AD, è possibile [ottenere una versione di valutazione di un mese](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene testato l'accesso SSO di Azure AD in un ambiente di test.

Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:

1. Aggiunta di RolePoint dalla raccolta
2. Configurazione e test dell'accesso Single Sign-On (SSO) di Microsoft Azure AD

## <a name="add-rolepoint-from-the-gallery"></a>Aggiungere RolePoint dalla raccolta
Per configurare l'integrazione di RolePoint in Azure AD, è necessario aggiungere RolePoint dalla raccolta al proprio elenco di app SaaS gestite.

**Per aggiungere RolePoint dalla raccolta, seguire questa procedura:**

1. Nel **portale di Azure classico** fare clic su **Active Directory** nel riquadro di spostamento sinistro. 

    ![Active Directory][1]

2. Nell'elenco **Directory** selezionare la directory per la quale si desidera abilitare l'integrazione delle directory.

3. Per aprire la visualizzazione applicazioni, nella visualizzazione directory fare clic su **Applications** nel menu superiore.

    ![Applications][2]

4. Fare clic su **Add** nella parte inferiore della pagina.

    ![Applicazioni][3]

5. Nella finestra di dialogo **Come procedere** fare clic su **Aggiungere un'applicazione dalla raccolta**.

    ![Applicazioni][4]

6. Nella casella di ricerca digitare **RolePoint**.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-rolepoint-tutorial/tutorial_rolepoint_001.png)

7. Nel riquadro dei risultati selezionare **RolePoint** e quindi fare clic su **Completa** per aggiungere l'applicazione.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-rolepoint-tutorial/tutorial_rolepoint_0001.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurare e testare l'accesso Single Sign-On di Azure AD
In questa sezione viene configurato e testato l'accesso SSO di Azure AD con RolePoint con un utente test di nome "Britta Simon".

Per il funzionamento dell'accesso SSO, Azure AD deve conoscere qual è l'utente di RolePoint che corrisponde a un utente di Azure AD. In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in RolePoint.

La relazione di collegamento viene stabilita assegnando il valore di **nome utente** in Azure AD come valore di **Username** (Nome utente) in RolePoint.

Per configurare e testare l'accesso SSO di Azure AD con RolePoint, è necessario completare i blocchi predefiniti seguenti:

1. **[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)**: per abilitare gli utenti all'uso di questa funzionalità.
2. **[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.
3. **[Creazione di un utente test RolePoint](#creating-a-rolepoint-test-user)**: per avere una controparte di Britta Simon in RolePoint collegata alla relativa rappresentazione in Azure AD.
4. **[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.
5. **[Test dell'accesso Single Sign-On](#testing-single-sign-on)**: per verificare se la configurazione funziona.

### <a name="configure-azure-ad-single-sign-on"></a>Configurare l'accesso Single Sign-On di Azure AD

Questa sezione descrive come abilitare l'accesso SSO di Azure AD nel portale di Azure classico e configurare l'accesso Single Sign-On nell'applicazione RolePoint.

L'applicazione RolePoint prevede che le asserzioni SAML abbiano un formato specifico. Configurare le attestazioni seguenti per questa applicazione. È possibile gestire i valori di questi attributi dalla scheda degli**attributi**dell'applicazione. La schermata seguente illustra un esempio relativo a questa operazione. 

![Configura accesso Single Sign-On](./media/active-directory-saas-rolepoint-tutorial/tutorial_rolepoint_01.png)

**Per configurare l'accesso Single Sign-On di Azure AD con RolePoint, seguire questa procedura:**

1. Nella pagina di integrazione dell'applicazione **RolePoint** del portale di Azure classico fare clic su **Attributi** nel menu in alto.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-rolepoint-tutorial/tutorial_rolepoint_02.png)

2. Nella finestra di dialogo **Attributi token SAML** seguire questa procedura per ciascuna riga della tabella:    

    | Nome attributo | Valore attributo |
    | --- | --- |    
    | FirstName | user.givenname |
    | LastName | user.surname |
    | Email | user.mail |
 
  1. Fare clic su **aggiungi attributo utente** per aprire la finestra di dialogo **Aggiungi attributo utente**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-rolepoint-tutorial/tutorial_rolepoint_03.png)
  2. Nella casella di testo **Nome attributo** , digitare il nome dell'attributo indicato per quella riga.
  3. Nell'elenco **Valore attributo** digitare il valore dell'attributo indicato per quella riga.
  4. Fare clic su **Completa**.

3. Nel menu in alto fare clic su **Avvio rapido**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-rolepoint-tutorial/tutorial_rolepoint_04.png) 

4. Nella pagina **Stabilire come si desidera che gli utenti accedano a RolePoint** selezionare **Single Sign-On di Azure AD** e quindi fare clic su **Avanti**.
 
    ![Configura accesso Single Sign-On](./media/active-directory-saas-rolepoint-tutorial/tutorial_rolepoint_05.png)

5. Nella pagina **Configurare le impostazioni dell'app** seguire questa procedura:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-rolepoint-tutorial/tutorial_rolepoint_06.png)
  1. Nella casella di testo **URL di accesso** digitare l'URL usando il modello seguente: `https://<company name>.rolepoint.com/login`
  2. Fare clic su **Avanti**.
  
    >[!NOTE] 
    >Si noti che questo non è il valore reale. È necessario aggiornare questo valore con l'URL di accesso effettivo. Per ottenere tale valore, contattare il [team di supporto di RolePoint](emaiLto:info@rolepoint.com).
    >

6. Nella pagina **Configure single sign-on at RolePoint (Configurare l'accesso Single Sign-On in RolePoint)** fare clic su **Download metadata (Scarica metadati)** e salvare il file sul computer:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-rolepoint-tutorial/tutorial_rolepoint_07.png) 

7. Per ottenere la configurazione dell'accesso Single Sign-On per l'applicazione, contattare il [team di supporto di RolePoint](emaiLto:info@rolepoint.com) e fornire i **metadati** scaricati.

8. Nel portale classico selezionare la conferma della configurazione dell'accesso Single Sign-On e quindi fare clic su **Avanti**.

    ![Single Sign-On di Microsoft Azure AD][10]

9. Nella pagina **Conferma Single Sign-on** fare clic su **Completa**.  
  
    ![Single Sign-On di Microsoft Azure AD][11]

### <a name="create-an-azure-ad-test-user"></a>Creare un utente test di Azure AD
Questa sezione descrive come creare un utente di test chiamato Britta Simon nel portale classico.

![Creare un utente di Azure AD][20]

**Per creare un utente test in Azure AD, eseguire la procedura seguente:**

1. Nel **portale di Azure classico** fare clic su **Active Directory** nel riquadro di spostamento sinistro.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-rolepoint-tutorial/create_aaduser_09.png) 

2. Nell'elenco **Directory** selezionare la directory per la quale si desidera abilitare l'integrazione delle directory.

3. Per visualizzare l'elenco di utenti, fare clic su **Utenti**nel menu in alto.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-rolepoint-tutorial/create_aaduser_03.png) 

4. Per aprire la finestra di dialogo **Aggiungi utente**, fare clic su **Aggiungi utente** nella barra degli strumenti in basso.
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-rolepoint-tutorial/create_aaduser_04.png) 

5. Nella pagina **Informazioni sull'utente** seguire questa procedura:
 
    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-rolepoint-tutorial/create_aaduser_05.png) 
 1. In Tipo di utente selezionare Nuovo utente nell'organizzazione.
 2. Nella casella di testo **Nome utente** digitare **BrittaSimon**.
 3. Fare clic su **Avanti**.

6.  Nella pagina **Profilo utente** seguire questa procedura:

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-rolepoint-tutorial/create_aaduser_06.png) 
 1. Nella casella di testo **Nome** digitare **Britta**. 
 2. Nella casella di testo **Cognome** digitare **Simon**.
 3. Nella casella di testo **Nome visualizzato** digitare **Britta Simon**.
 4. Nell'elenco **Ruolo** selezionare **Utente**.
 5. Fare clic su **Avanti**.

7. Nella pagina **Ottieni password temporanea** fare clic su **crea**.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-rolepoint-tutorial/create_aaduser_07.png) 

8. Nella pagina **Ottieni password temporanea** seguire questa procedura:

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-rolepoint-tutorial/create_aaduser_08.png) 
 1. Prendere nota del valore visualizzato in **Nuova password**.
 2. Fare clic su **Complete**.   

### <a name="create-a-rolepoint-test-user"></a>Creare un utente test di RolePoint

In questa sezione viene creato un utente chiamato Britta Simon in RolePoint. Collaborare con il [team di supporto di RolePoint](emaiLto:info@rolepoint.com) per aggiungere utenti nella piattaforma RolePoint.

### <a name="assign-the-azure-ad-test-user"></a>Assegnare l'utente test di Azure AD

In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a RolePoint.

![Assegna utente][200] 

**Per assegnare Britta Simon a RolePoint, seguire questa procedura:**

1. Per aprire la visualizzazione delle applicazioni nel portale classico, nella visualizzazione Directory fare clic su **Applicazioni** nel menu in alto.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni selezionare **RolePoint**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-rolepoint-tutorial/tutorial_rolepoint_50.png) 

3. Scegliere **Utenti**dal menu in alto.

    ![Assegna utente][203] 

4. Nell'elenco di utenti selezionare **Britta Simon**.

5. Fare clic su **Assegna**sulla barra degli strumenti in basso.
    
    ![Assegna utente][205]

### <a name="test-single-sign-on"></a>Testare l'accesso Single Sign-On

In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.

Quando si fa clic sul riquadro RolePoint nel pannello di accesso, si dovrebbe accedere automaticamente all'applicazione RolePoint.

## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_205.png

