---
title: 'Esercitazione: Integrazione di Azure Active Directory con Dow Jones Factiva | Microsoft Docs'
description: Informazioni su come configurare l&quot;accesso Single Sign-On tra Azure Active Directory e Dow Jones Factiva.
services: active-directory
documentationCenter: na
authors: jeevansd
manager: femila
ms.assetid: b36e97e8-37a6-4096-a894-530427ee1331
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/17/2016
ms.author: jeedes
translationtype: Human Translation
ms.sourcegitcommit: be14d8a3acc04cdc83daeebf439498aa78f8d3a6
ms.openlocfilehash: df461ff2c58fb0e66c112d2bfd4618ef2fc4f6ac


---


# <a name="tutorial-azure-active-directory-integration-with-dow-jones-factiva"></a>Esercitazione: Integrazione di Azure Active Directory con Dow Jones Factiva

Questa esercitazione descrive come integrare Dow Jones Factiva con Azure Active Directory (Azure AD).

L'integrazione di Dow Jones Factiva con Azure AD offre i vantaggi seguenti:

- È possibile controllare in Azure AD chi può accedere a Dow Jones Factiva
- È possibile abilitare gli utenti per l'accesso automatico ad Dow Jones Factiva (Single Sign-On) con i propri account Azure AD
- È possibile gestire gli account da una posizione centrale: il portale di Azure classico

Per altre informazioni sull'integrazione di app SaaS con Azure AD, vedere [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prerequisiti

Per configurare l'integrazione di Azure AD con Dow Jones Factiva, sono necessari gli elementi seguenti:

- Sottoscrizione di Azure AD.
- Sottoscrizione di Dow Jones Factiva abilitata per l'accesso Single Sign-On


> [!NOTE] 
> Non è consigliabile usare un ambiente di produzione per testare i passaggi di questa esercitazione.


A questo scopo, è consigliabile seguire le indicazioni seguenti:

- Non usare l'ambiente di produzione, a meno che non sia necessario.
- Se non si dispone di un ambiente di prova di Azure AD, è possibile ottenere una versione di valutazione di un mese [qui](https://azure.microsoft.com/pricing/free-trial/).


## <a name="scenario-description"></a>Descrizione dello scenario
In questa esercitazione viene eseguito il test dell'accesso Single Sign-On di Azure AD in un ambiente di test.

Lo scenario descritto in questa esercitazione prevede i due blocchi predefiniti seguenti:

1. Aggiunta di Dow Jones Factiva dalla raccolta
2. Configurazione e test dell'accesso Single Sign-On di Azure AD


## <a name="adding-dow-jones-factiva-from-the-gallery"></a>Aggiunta di Dow Jones Factiva dalla raccolta
Per configurare l'integrazione di Dow Jones Factiva in Azure AD, è necessario aggiungerla dalla raccolta al proprio elenco di app SaaS gestite.

**Per aggiungere Dow Jones Factiva dalla raccolta, seguire questa procedura:**

1. Nel **portale di Azure classico**fare clic su **Active Directory**nel riquadro di spostamento sinistro.

    ![Active Directory][1]
2. Nell'elenco **Directory** selezionare la directory per la quale si desidera abilitare l'integrazione delle directory.

3. Per aprire la visualizzazione applicazioni, nella visualizzazione directory fare clic su **Applications** nel menu superiore.

    ![Applications][2]

4. Fare clic su **Add** nella parte inferiore della pagina.

    ![Applicazioni][3]

5. Nella finestra di dialogo **Come procedere** fare clic su **Aggiungere un'applicazione dalla raccolta**.

    ![Applicazioni][4]

6. Nella casella di ricerca digitare **Dow Jones Factiva**.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_dowjonesfactiva_01.png)

7. Nel riquadro dei risultati selezionare **Dow Jones Factiva** e quindi fare clic su **Completa** per aggiungere l'applicazione.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_dowjonesfactiva_02.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configurazione e test dell'accesso Single Sign-On di Azure AD
In questa sezione viene configurato e testato l'accesso Single Sign-On di Azure AD con Dow Jones Factiva usando un utente test di nome "Britta Simon".

Per il funzionamento dell'accesso Single Sign-On, Azure AD deve conoscere qual è l'utente di Dow Jones Factiva che corrisponde a un utente di Azure AD. In altre parole, deve essere stabilita una relazione di collegamento tra un utente di Azure AD e l'utente correlato in Dow Jones Factiva.

La relazione di collegamento viene stabilita assegnando il valore di **nome utente** in Azure AD come valore di **Nomeutente** in Dow Jones Factiva.

Per configurare e testare l'accesso Single Sign-On di Azure AD con Dow Jones Factiva, è necessario completare i blocchi predefiniti seguenti:

1. **[Configurazione dell'accesso Single Sign-On di Azure AD](#configuring-azure-ad-single-sign-on)** : per abilitare gli utenti all'uso di questa funzionalità.
2. **[Creazione di un utente test di Azure AD](#creating-an-azure-ad-test-user)** : per testare l'accesso Single Sign-On di Azure AD con l'utente Britta Simon.
3. **[Creazione di un utente test di Dow Jones Factiva](#creating-a-dowjones-factiva-test-user)**: per avere una controparte di Britta Simon in Dow Jones Factiva collegata alla relativa rappresentazione in Azure AD.
4. **[Assegnazione dell'utente test di Azure AD](#assigning-the-azure-ad-test-user)** : per abilitare Britta Simon all'uso dell'accesso Single Sign-On di Azure AD.
5. **[Testing Single Sign-On](#testing-single-sign-on)** : per verificare se la configurazione funziona.

### <a name="configuring-azure-ad-single-sign-on"></a>Configurazione dell'accesso Single Sign-On di Azure AD

In questa sezione viene abilitato l'accesso Single Sign-On di Azure AD nel portale classico e viene configurato l'accesso Single Sign-On nell'applicazione Dow Jones Factiva.


**Per configurare l'accesso Single Sign-On di Azure AD con Dow Jones Factiva, seguire questa procedura:**

1. Nella pagina di integrazione dell'applicazione **Dow Jones Factiva** del Portale di Azure classico fare clic su **Configura accesso Single Sign-On** per aprire la finestra di dialogo **Configura accesso Single Sign-On**.
     
    ![Configura accesso Single Sign-On][6] 

2. Nella pagina **How would you like users to sign on to Dow Jones Factiva (Stabilire come si desidera che gli utenti accedano a Dow Jones Factiva)** selezionare **Azure AD Single Sign-On (Single Sign-On di Azure AD)** e quindi fare clic su **Avanti**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_dowjonesfactiva_03.png) 

3. Nella pagina **Configurare le impostazioni dell'app** seguire questa procedura:
    
    a. click **Avanti**
 
4. Nella pagina **Configure single sign-on at Dow Jones Factiva (Configura accesso Single Sign-On in Dow Jones Factiva)** seguire questa procedura:

    ![Configura accesso Single Sign-On](./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_dowjonesfactiva_05.png)

    a. Fare clic su **Scarica metadati**e quindi salvare il file nel computer.

    b. Fare clic su **Avanti**.


5. Per ottenere l'accesso Single Sign-On configurato per l'applicazione, contattare il team di supporto di Dow Jones Factiva e fornire i seguenti elementi:

    • Il file dei **metadati**

6. Nel portale di Azure classico selezionare la conferma della configurazione e quindi fare clic su **Avanti**.
    
    ![Single Sign-On di Microsoft Azure AD][10]

7. Nella pagina **Conferma Single Sign-on** fare clic su **Completa**.  
 
    ![Single Sign-On di Microsoft Azure AD][11]


### <a name="creating-an-azure-ad-test-user"></a>Creazione di un utente test di Azure AD
In questa sezione viene creato un utente test chiamato Britta Simon nel portale classico.


![Creare un utente di Azure AD][20]

**Per creare un utente test in Azure AD, eseguire la procedura seguente:**

1. Nel **portale di Azure classico** fare clic su **Active Directory** nel riquadro di spostamento sinistro.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-dowjones-factiva-tutorial/create_aaduser_09.png) 

2. Nell'elenco **Directory** selezionare la directory per la quale si desidera abilitare l'integrazione delle directory.

3. Per visualizzare l'elenco di utenti, fare clic su **Utenti**nel menu in alto.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-dowjones-factiva-tutorial/create_aaduser_03.png) 

4. Per aprire la finestra di dialogo **Aggiungi utente**, fare clic su **Aggiungi utente** nella barra degli strumenti in basso.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-dowjones-factiva-tutorial/create_aaduser_04.png) 

5. Nella pagina **Informazioni sull'utente** seguire questa procedura:  ![Creazione di un utente test di Azure AD](./media/active-directory-saas-dowjones-factiva-tutorial/create_aaduser_05.png) 

    a. In Tipo di utente selezionare Nuovo utente nell'organizzazione.

    b. Nella casella di testo **Nome utente** digitare **BrittaSimon**.

    c. Fare clic su **Avanti**.

6.  Nella pagina **Profilo utente** seguire questa procedura: ![Creazione di un utente test di Azure AD](./media/active-directory-saas-dowjones-factiva-tutorial/create_aaduser_06.png) 

    a. Nella casella di testo **Nome** digitare **Britta**.  

    b. Nella casella di testo **Cognome** digitare **Simon**.

    c. Nella casella di testo **Nome visualizzato** digitare **Britta Simon**.

    d. Nell'elenco **Ruolo** selezionare **Utente**.

    e. Fare clic su **Avanti**.

7. Nella pagina **Ottieni password temporanea** fare clic su **crea**.

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-dowjones-factiva-tutorial/create_aaduser_07.png) 

8. Nella pagina **Ottieni password temporanea** seguire questa procedura:

    ![Creazione di un utente test di Azure AD](./media/active-directory-saas-dowjones-factiva-tutorial/create_aaduser_08.png) 

    a. Prendere nota del valore visualizzato in **Nuova password**.

    b. Fare clic su **Completa**.   



### <a name="creating-an-dow-jones-factiva-test-user"></a>Creazione di un utente test Dow Jones Factiva

In questa sezione viene creato un utente di nome Britta Simon in Dow Jones Factiva. Collaborare con il team di supporto di Dow Jones Factiva per aggiungere gli utenti nella piattaforma Dow Jones Factiva.


### <a name="assigning-the-azure-ad-test-user"></a>Assegnazione dell'utente test di Azure AD

In questa sezione Britta Simon viene abilitata per l'uso dell'accesso Single Sign-On di Azure concedendole l'accesso a Dow Jones Factiva.

![Assegna utente][200] 

**Per assegnare Britta Simon a Dow Jones Factiva, seguire questa procedura:**

1. Per aprire la visualizzazione delle applicazioni nel portale classico, nella visualizzazione directory fare clic su **Applicazioni** nel menu in alto.

    ![Assegna utente][201] 

2. Nell'elenco di applicazioni, selezionare **Dow Jones Factiva**.

    ![Configura accesso Single Sign-On](./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_dowjonesfactiva_50.png) 

3. Scegliere **Utenti**dal menu in alto.

    ![Assegna utente][203]

4. Nell'elenco di utenti selezionare **Britta Simon**.

5. Fare clic su **Assegna**sulla barra degli strumenti in basso.

    ![Assegna utente][205]


### <a name="testing-single-sign-on"></a>Test dell'accesso Single Sign-On

In questa sezione viene testata la configurazione dell'accesso Single Sign-On di Azure AD usando il pannello di accesso.

Quando si fa clic sul riquadro di Dow Jones Factiva nel riquadro di accesso, si dovrebbe accedere automaticamente all'applicazione Dow Jones Factiva.


## <a name="additional-resources"></a>Risorse aggiuntive

* [Elenco di esercitazioni sulla procedura di integrazione delle app SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Informazioni sull'accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_205.png



<!--HONumber=Nov16_HO4-->


