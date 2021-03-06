---
title: Criteri di autenticazione di Gestione API di Azure | Documentazione Microsoft
description: Informazioni sui criteri di autenticazione disponibili per l&quot;uso in Gestione API di Azure.
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 061702a7-3a78-472b-a54a-f3b1e332490d
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
translationtype: Human Translation
ms.sourcegitcommit: 77fd7b5b339a8ede8a297bec96f91f0a243cc18d
ms.openlocfilehash: f447e43799e56114d52b0dc0f5c36265f2870c8e

---
# <a name="api-management-authentication-policies"></a>Criteri di autenticazione di Gestione API di Azure
Questo argomento fornisce un riferimento per i seguenti criteri di Gestione API. Per informazioni sull'aggiunta e sulla configurazione dei criteri, vedere [Criteri di Gestione API](http://go.microsoft.com/fwlink/?LinkID=398186).  
  
##  <a name="a-nameauthenticationpoliciesa-authentication-policies"></a><a name="AuthenticationPolicies"></a> Criteri di autenticazione  
  
-   [Autenticazione con base](api-management-authentication-policies.md#Basic): consente di eseguire l'autenticazione con un servizio back-end tramite l'autenticazione di base.  
  
-   [Autenticazione con certificato](api-management-authentication-policies.md#ClientCertificate): consente di eseguire l'autenticazione con un servizio back-end tramite certificati client.  
  
##  <a name="a-namebasica-authenticate-with-basic"></a><a name="Basic"></a> Autenticazione con base  
 Usare il criterio `authentication-basic` per eseguire l'autenticazione con un servizio di back-end tramite l'autenticazione di base. Questo criterio imposta l'intestazione di autorizzazione HTTP sul valore corrispondente alle credenziali specificate nei criteri.  
  
### <a name="policy-statement"></a>Istruzione del criterio  
  
```xml  
<authentication-basic username="username" password="password" />  
```  
  
### <a name="example"></a>Esempio  
  
```xml  
<authentication-basic username="testuser" password="testpassword" />  
```  
  
### <a name="elements"></a>Elementi  
  
|Nome|Descrizione|Obbligatorio|  
|----------|-----------------|--------------|  
|authentication-basic|Elemento radice.|Sì|  
  
### <a name="attributes"></a>Attributi  
  
|Nome|Descrizione|Obbligatorio|Default|  
|----------|-----------------|--------------|-------------|  
|username|Specifica il nome utente della credenziale di base.|Sì|N/D|  
|password|Specifica la password della credenziale di base.|Sì|N/D|  
  
### <a name="usage"></a>Utilizzo  
 Questo criterio può essere usato nelle [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e negli [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) seguenti del criterio.  
  
-   **Sezioni del criterio:** in ingresso  
  
-   **Ambiti del criterio:** API  
  
##  <a name="a-nameclientcertificatea-authenticate-with-client-certificate"></a><a name="ClientCertificate"></a> Autenticazione con certificato client  
 Usare il criterio `authentication-certificate` per eseguire l'autenticazione con un servizio di back-end tramite il certificato client. Il certificato deve essere prima [installato in Gestione API](http://go.microsoft.com/fwlink/?LinkID=511599) e viene identificato tramite la relativa identificazione personale.  
  
### <a name="policy-statement"></a>Istruzione del criterio  
  
```xml  
<authentication-certificate thumbprint="thumbprint" />  
```  
  
### <a name="example"></a>Esempio  
  
```xml  
<authentication-certificate thumbprint="....." />  
```  
  
### <a name="elements"></a>Elementi  
  
|Nome|Descrizione|Obbligatorio|  
|----------|-----------------|--------------|  
|authentication-certificate|Elemento radice.|Sì|  
  
### <a name="attributes"></a>Attributi  
  
|Nome|Descrizione|Obbligatorio|Default|  
|----------|-----------------|--------------|-------------|  
|thumbprint|Identificazione personale del certificato client.|Sì|N/D|  
  
### <a name="usage"></a>Utilizzo  
 Questo criterio può essere usato nelle [sezioni](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e negli [ambiti](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) seguenti del criterio.  
  
-   **Sezioni del criterio:** in ingresso  
  
-   **Ambiti del criterio:** API  
  

## <a name="next-steps"></a>Passaggi successivi
Per altre informazioni sull'uso dei criteri, vedere [Criteri di Gestione API](api-management-howto-policies.md).  


<!--HONumber=Jan17_HO2-->


