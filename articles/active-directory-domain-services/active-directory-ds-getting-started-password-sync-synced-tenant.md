---
title: 'Azure AD Domain Services: abilitare la sincronizzazione password | Documentazione Microsoft'
description: Introduzione a Servizi di dominio Azure Active Directory
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 8731f2b2-661c-4f3d-adba-2c9e06344537
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/17/2017
ms.author: maheshu
translationtype: Human Translation
ms.sourcegitcommit: bb1ca3189e6c39b46eaa5151bf0c74dbf4a35228
ms.openlocfilehash: 4969b43831a3813a4e76c6447c252a9c458f371a
ms.lasthandoff: 03/18/2017


---
# <a name="enable-password-synchronization-to-azure-ad-domain-services"></a>Abilitare la sincronizzazione password in Servizi di dominio Azure AD
Nelle attività precedenti si è abilitato Servizi di dominio Azure AD per il tenant di Azure AD. L'attività successiva consiste nell'abilitare la sincronizzazione delle password in Servizi di dominio Azure AD. Dopo avere configurato la sincronizzazione delle credenziali, gli utenti possono accedere al dominio gestito usando le credenziali aziendali.

I passaggi sono diversi a seconda che l'organizzazione abbia un tenant di Azure AD basato solo sul cloud o sia impostata per la sincronizzazione con la directory locale tramite Azure AD Connect.

<br>

> [!div class="op_single_selector"]
> * [Tenant di Azure AD solo cloud](active-directory-ds-getting-started-password-sync.md)
> * [Tenant di Azure AD sincronizzato](active-directory-ds-getting-started-password-sync-synced-tenant.md)
>
>

<br>

## <a name="task-5-enable-password-synchronization-to-aad-domain-services-for-a-synced-azure-ad-tenant"></a>Attività 5: Abilitare la sincronizzazione password in Servizi di dominio Azure AD per un tenant di Azure AD sincronizzato
Un tenant di Azure AD viene impostato per la sincronizzazione con la directory locale dell'organizzazione con Azure AD Connect. Per impostazione predefinita, Azure AD Connect non sincronizza gli hash delle credenziali NTLM e Kerberos con Azure AD. Per usare Servizi di dominio Azure AD, è necessario configurare Azure AD Connect per sincronizzare gli hash delle credenziali necessari per l'autenticazione NTLM e Kerberos. 

> [!WARNING]
> È NECESSARIO abilitare la sincronizzazione password in Azure AD Domain Services ogni volta che si abilita Azure AD Domain Services. Azure AD Domain Services potrebbe essere già stato abilitato per l'istanza di Azure AD Directory ed essere stato successivamente disabilitato. Alla successiva abilitazione di Azure AD Domain Services per la directory, è comunque necessario abilitare la sincronizzazione password.
>
>

I passaggi seguenti consentono di sincronizzare gli hash delle credenziali necessari con il tenant di Azure AD.

### <a name="install-or-update-azure-ad-connect"></a>Installare o aggiornare Azure AD Connect
Installare l'ultima versione consigliata di Azure AD Connect in un computer aggiunto a un dominio. Se esiste già un'istanza del programma di installazione di Azure AD Connect, è necessario aggiornarla per usare la versione più recente di Azure AD Connect. Per evitare problemi o bug noti che potrebbero essere già stati corretti, assicurarsi di usare sempre la versione più recente di Azure AD Connect.

**[Scaricare Azure AD Connect](http://www.microsoft.com/download/details.aspx?id=47594)**

Versione consigliata: **1.1.281.0** , pubblicata il 7 settembre 2016.

> [!WARNING]
> L'installazione dell'ultima versione consigliata di Azure AD Connect è NECESSARIA per abilitare le credenziali di password legacy (obbligatorio per l'autenticazione NTLM e Kerberos) da sincronizzare nel tenant di Azure AD. Questa funzionalità non è disponibile nelle versioni precedenti di Azure AD Connect o con lo strumento DirSync legacy.
>
>

Le istruzioni per l'installazione di Azure AD Connect sono disponibili nell'articolo [Introduzione ad Azure AD Connect](../active-directory/active-directory-aadconnect.md)

### <a name="enable-synchronization-of-ntlm-and-kerberos-credential-hashes-to-azure-ad"></a>Abilitare la sincronizzazione di hash di credenziali NTLM e Kerberos in Azure AD
Eseguire lo script di PowerShell seguente in ogni foresta di Active Directory per forzare la sincronizzazione password completa e abilitare la sincronizzazione degli hash delle credenziali degli utenti locali con il tenant di Azure AD. Questo script consente di sincronizzare gli hash delle credenziali necessari per l'autenticazione NTLM/Kerberos con il tenant di Azure AD.

```
$adConnector = "<CASE SENSITIVE AD CONNECTOR NAME>"  
$azureadConnector = "<CASE SENSITIVE AZURE AD CONNECTOR NAME>"  
Import-Module adsync  
$c = Get-ADSyncConnector -Name $adConnector  
$p = New-Object Microsoft.IdentityManagement.PowerShell.ObjectModel.ConfigurationParameter "Microsoft.Synchronize.ForceFullPasswordSync", String, ConnectorGlobal, $null, $null, $null
$p.Value = 1  
$c.GlobalParameters.Remove($p.Name)  
$c.GlobalParameters.Add($p)  
$c = Add-ADSyncConnector -Connector $c  
Set-ADSyncAADPasswordSyncConfiguration -SourceConnector $adConnector -TargetConnector $azureadConnector -Enable $false   
Set-ADSyncAADPasswordSyncConfiguration -SourceConnector $adConnector -TargetConnector $azureadConnector -Enable $true  
```

A seconda delle dimensioni della directory (numero di utenti, gruppi e così via), la sincronizzazione degli hash delle credenziali con Azure AD richiede tempo. Le password saranno utilizzabili nel dominio gestito dei servizi di dominio Azure Active Directory non appena le hash di credenziali saranno sincronizzate con Azure.

<br>

## <a name="related-content"></a>Contenuti correlati
* [Abilitare la sincronizzazione password in Servizi di dominio Azure AD per una directory di Azure AD solo cloud](active-directory-ds-getting-started-password-sync.md)
* [Amministrare un dominio gestito di Servizi di dominio Azure AD](active-directory-ds-admin-guide-administer-domain.md)
* [Aggiungere una macchina virtuale Windows a un dominio gestito di Servizi di dominio Azure AD](active-directory-ds-admin-guide-join-windows-vm.md)
* [Aggiungere una macchina virtuale Red Hat Enterprise Linux a un dominio gestito di Servizi di dominio Azure AD](active-directory-ds-admin-guide-join-rhel-linux-vm.md)

