---
title: 'Esercitazione: Integrazione di Azure Active Directory con SugarCRM | Microsoft Docs'
description: Informazioni su come usare SugarCRM con Azure Active Directory per abilitare l&quot;accesso Single Sign-On, il provisioning automatizzato e altro ancora.
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 3331b9fc-ebc0-4a3a-9f7b-bf20ee35d180
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 3/07/2017
ms.author: jeedes
translationtype: Human Translation
ms.sourcegitcommit: 07635b0eb4650f0c30898ea1600697dacb33477c
ms.openlocfilehash: acd11de9f2b987c3c0bc6d74cff8019aca92f437
ms.lasthandoff: 03/28/2017


---
# <a name="tutorial-azure-active-directory-integration-integration-with-sugarcrm"></a>Esercitazione: Integrazione di Azure Active Directory con SugarCRM
In questa esercitazione verrà descritta l'integrazione di Azure e Sugar CRM.  

Per lo scenario descritto in questa esercitazione si presuppone che l'utente disponga di quanto segue:

* Sottoscrizione di Azure valida
* Sottoscrizione di Sugar CRM abilitata per l'accesso Single Sign-On (SSO)

Al termine dell'esercitazione, gli utenti di Azure AD assegnati a Sugar CRM potranno accedere all'applicazione usando SSO tramite il sito aziendale di Sugar CRM (accesso avviato dal provider di servizi) o seguendo le istruzioni riportate in [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).

Lo scenario descritto in questa esercitazione include i blocchi predefiniti seguenti:

1. Abilitazione dell'integrazione dell'applicazione Sugar CRM
2. Configurazione dell'accesso Single Sign-On (SSO)
3. Configurazione del provisioning utente
4. Assegnazione degli utenti

![Scenario](./media/active-directory-saas-sugarcrm-tutorial/IC795881.png "Scenario")

## <a name="enable-the-application-integration-for-sugar-crm"></a>Abilitare l'integrazione dell'applicazione per Sugar CRM
In questa sezione viene descritto come abilitare l'integrazione dell'applicazione per Sugar CRM.

**Per abilitare l'integrazione dell'applicazione per Sugar CRM, eseguire la procedura seguente:**

1. Nel portale di Azure classico fare clic su **Active Directory**nel riquadro di spostamento sinistro.
   
    ![Active Directory](./media/active-directory-saas-sugarcrm-tutorial/IC700993.png "Active Directory")

2. Nell'elenco **Directory** selezionare la directory per la quale si desidera abilitare l'integrazione delle directory.

3. Per aprire la visualizzazione applicazioni, nella visualizzazione directory fare clic su **Applications** nel menu superiore.
   
    ![Applicazioni](./media/active-directory-saas-sugarcrm-tutorial/IC700994.png "Applicazioni")

4. Fare clic su **Add** nella parte inferiore della pagina.
   
    ![Aggiungere un'applicazione](./media/active-directory-saas-sugarcrm-tutorial/IC749321.png "Aggiungere un'applicazione")

5. Nella finestra di dialogo **Come procedere** fare clic su **Aggiungere un'applicazione dalla raccolta**.
   
    ![Aggiungere un'applicazione dalla raccolta](./media/active-directory-saas-sugarcrm-tutorial/IC749322.png "Aggiungere un'applicazione dalla raccolta")

6. Nella **casella di ricerca**, digitare **Sugar CRM**.
   
    ![Raccolta di applicazioni](./media/active-directory-saas-sugarcrm-tutorial/IC795882.png "Raccolta di applicazioni")

7. Nel riquadro dei risultati selezionare **Sugar CRM**, quindi fare clic su **Completa** per aggiungere l'applicazione.
   
    ![Sugar CRM](./media/active-directory-saas-sugarcrm-tutorial/IC795883.png "Sugar CRM")

## <a name="configure-single-sign-on"></a>Configura accesso Single Sign-On
In questa sezione viene descritto come consentire agli utenti di eseguire l'autenticazione a Sugar CRM tramite il proprio account in Azure AD utilizzando la federazione basata sul protocollo SAML.  

Come parte di questa procedura, verrà richiesto di caricare un file di certificato codificato in base 64 sul proprio tenant Sugar CRM.  

Se non si ha familiarità con questa procedura, vedere il video che descrive [come convertire un certificato binario in un file di testo](http://youtu.be/PlgrzUZ-Y1o)

**Per configurare l'accesso Single Sign-On, seguire questa procedura:**

1. Nella pagina di integrazione dell'applicazione **Sugar CRM** del portale di Azure classico fare clic su **Configura accesso Single Sign-On** per aprire la finestra di dialogo **Configura accesso Single Sign-On**.
   
    ![Configurare l'accesso Single Sign-On](./media/active-directory-saas-sugarcrm-tutorial/IC795884.png "Configurare l'accesso Single Sign-On")

2. Nella pagina **Stabilire come si desidera che gli utenti accedano a Sugar CRM** selezionare **Single Sign-On di Microsoft Azure AD**, quindi fare clic su **Avanti**.
   
    ![Configurare l'accesso Single Sign-On](./media/active-directory-saas-sugarcrm-tutorial/IC795885.png "Configurare l'accesso Single Sign-On")

3. Nella casella di testo **URL di accesso Sugar CRM** della pagina **Configura URL app** digitare l'URL usato dagli utenti per accedere all'applicazione Sugar CRM, ad esempio "*http://company.sugarondemand.com*", quindi fare clic su **Avanti**.
   
    ![Configurare l'URL dell'app](./media/active-directory-saas-sugarcrm-tutorial/IC795886.png "Configurare l'URL dell'app")

4. Nella pagina **Configura accesso Single Sign-On in Sugar CRM** per scaricare il file del certificato, fare clic su **Scarica certificato**, quindi salvare il certificato nel computer.
   
    ![Configurare l'accesso Single Sign-On](./media/active-directory-saas-sugarcrm-tutorial/IC796918.png "Configurare l'accesso Single Sign-On")

5. In un'altra finestra del browser Web accedere al sito aziendale di Sugar CRM come amministratore.

6. Passare alla pagina **Admin**.
   
    ![Amministratore](./media/active-directory-saas-sugarcrm-tutorial/IC795888.png "Amministratore")

7. Nella sezione **Amministrazione**, fare clic su **Gestione password**.
   
    ![Amministrazione](./media/active-directory-saas-sugarcrm-tutorial/IC795889.png "Amministrazione")

8. Selezionare **Abilita autenticazione SAML**.
   
    ![Amministrazione](./media/active-directory-saas-sugarcrm-tutorial/IC795890.png "Amministrazione")

9. Nella sezione **SAML Authentication** seguire questa procedura:
   
    ![Autenticazione SAML](./media/active-directory-saas-sugarcrm-tutorial/IC795891.png "Autenticazione SAML")   
  1. Nella finestra di dialogo **Configura accesso Single Sign-On in Sugar CRM** del portale di Azure classico copiare il valore di **URL accesso remoto** e incollarlo nella casella di testo **URL di accesso**.
  2. Nella finestra di dialogo **Configura accesso Single Sign-On in Sugar CRM** del portale di Azure classico copiare il valore di **URL accesso remoto** e incollarlo nella casella di testo **URL SLO**.
  3. Creare un file **con codifica Base 64** dal certificato scaricato.
      
     >[!TIP]
     >Per informazioni dettagliate, vedere il video che illustra [come convertire un certificato binario in un file di testo](http://youtu.be/PlgrzUZ-Y1o). 
     > 

  4. Aprire il certificato con codifica Base 64 nel Blocco note, copiarne il contenuto negli Appunti e incollare l’intero certificato nella casella di testo **Certificate X.509** .
  5. Fare clic su **Save**.

10. Nella finestra di dialogo **Configura accesso Single Sign-On in Sugar CRM** del portale di Azure classico selezionare la conferma della configurazione dell'accesso Single Sign-On, quindi fare clic su **Completa**.
    
    ![Configurare l'accesso Single Sign-On](./media/active-directory-saas-sugarcrm-tutorial/IC796919.png "Configurare l'accesso Single Sign-On")

## <a name="configure-user-provisioning"></a>Configura provisioning utenti
Per consentire agli utenti di Azure AD di accedere a Sugar CRM, è necessario eseguirne il provisioning in Sugar CRM.

Nel caso di Sugar CRM, il provisioning è un'attività manuale.

**Per effettuare il provisioning di un account utente, seguire questa procedura:**

1. Accedere al sito aziendale di **Sugar CRM** come amministratore.
2. Passare alla pagina **Admin**.
   
    ![Amministratore](./media/active-directory-saas-sugarcrm-tutorial/IC795888.png "Amministratore")

3. Nella sezione **Administration** (Amministrazione) fare clic su **User Management** (Gestione utenti).
   
    ![Amministrazione](./media/active-directory-saas-sugarcrm-tutorial/IC795893.png "Amministrazione")

4. Passare a **Users \> Create New User** (Utenti > Crea nuovo utente).
   
    ![Creazione di un nuovo utente](./media/active-directory-saas-sugarcrm-tutorial/IC795894.png "Creazione di un nuovo utente")

5. Nella scheda **Profilo utente** eseguire la procedura seguente:
   
    ![Nuovo utente](./media/active-directory-saas-sugarcrm-tutorial/IC795895.png "Nuovo utente")
  * Digitare il nome utente, il cognome e l’indirizzo e-mail di utente di Azure Active Directory valido nelle caselle di testo correlate.
6. Per **Status** (Stato) selezionare **Active** (Attivo).

7. Nella scheda Password, eseguire la procedura seguente:
   
    ![Nuovo utente](./media/active-directory-saas-sugarcrm-tutorial/IC795896.png "Nuovo utente")
  1. Digitare la password nella casella di controllo correlata.
  2. Fare clic su **Save**.

>[!NOTE]
>È possibile usare qualsiasi altro strumento di creazione di account utente Sugar CRM o qualsiasi API fornita da Sugar CRM per eseguire il provisioning degli account utente di Azure AD. 
> 

## <a name="assign-users"></a>Assegna utenti
Per testare la configurazione, è necessario concedere l'accesso all'applicazione agli utenti di Azure AD a cui si vuole consentirne l'uso, assegnando tali utenti all'applicazione.

**Per assegnare gli utenti a Sugar CRM, eseguire la procedura seguente:**

1. Nel portale di Azure classico creare un account di test.

2. Nella pagina di integrazione di **Sugar CRM**, fare clic su **Assegna utenti**.
   
    ![Assegnare utenti](./media/active-directory-saas-sugarcrm-tutorial/IC795897.png "Assegnare utenti")

3. Selezionare l'utente di test, fare clic su **Assegna** e quindi su **Sì** per confermare l'assegnazione.
   
    ![Sì](./media/active-directory-saas-sugarcrm-tutorial/IC767830.png "Sì")

Per testare le impostazioni di Single Sign-On, aprire il pannello di accesso. Per altre informazioni sul pannello di accesso, vedere [Introduzione al Pannello di accesso](active-directory-saas-access-panel-introduction.md).


