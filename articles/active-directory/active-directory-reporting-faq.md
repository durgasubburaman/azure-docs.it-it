---
title: Domande frequenti sulla creazione di report in Azure Active Directory | Documentazione Microsoft
description: Domande frequenti sulla creazione di report in Azure Active Directory.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 534da0b1-7858-4167-9986-7a62fbd10439
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.translationtype: Human Translation
ms.sourcegitcommit: e6dcd3f6f9c7c8765409c3b0d50e4b3843bab5c6
ms.openlocfilehash: e39ee63d190308b87ebeb43adeb8b3e5db86df57
ms.contentlocale: it-it
ms.lasthandoff: 02/22/2017


---
# <a name="azure-active-directory-reporting-faq"></a>Domande frequenti sulla creazione di report in Azure Active Directory

Questo articolo include risposte alle domande frequenti sulla creazione di report in Azure Active Directory.  
Per altre informazioni, vedere la pagina relativa alla [creazione di report in Azure Active Directory](active-directory-reporting-azure-portal.md) 

**D: Qual è la conservazione dei dati per i log attività (controllo e accessi) nel portale di Azure?** 

**R:** Offriamo 7 giorni di dati per i clienti con sottoscrizione gratuita. Passando a una licenza AD Premium 1 o Azure AD Premium 2 è possibile accedere ai dati fino a 30 giorni. Per altri dettagli sulla conservazione, vedere la pagina relativa ai [criteri di conservazione dei report di Azure Active Directory](active-directory-reporting-retention.md).

--- 

**D: Quanto tempo occorre per la visualizzazione dei dati sull'attività dopo il completamento della stessa?**

**R:** I log dell'attività di controllo hanno una latenza compresa tra 15 minuti e un'ora. I log dell'attività di accesso hanno una latenza compresa tra 15 minuti per la maggior parte dei record e fino a 2 ore per altri record.

---

**Q: È necessario essere amministratore globale per visualizzare i log attività nel portale di Azure o per ottenere i dati tramite l'API?**

**R:** No. L'utente può avere un **ruolo con autorizzazioni di lettura per la sicurezza**, può essere un **amministratore della protezione** o un **amministratore globale** per visualizzare i dati dei report nel portale di Azure o accedendovi tramite l'API.

---

**D: È possibile ottenere informazioni sui log attività di Office 365 tramite il portale di Azure?**

**R:** Sebbene l'attività di Office 365 e i log attività di Azure AD condividano numerose risorse della directory, se si desidera una visualizzazione completa dei log attività di Office 365, è necessario usare l'interfaccia di amministrazione di Office 365 per ottenere informazioni sui log attività di Office 365.

---


**D: Quali API è necessario usare per ottenere informazioni sui log attività di Office 365?**

**R:** Usare le API Gestione di Office 365 per accedere ai [log attività di Office 365 tramite un'API](https://msdn.microsoft.com/office-365/office-365-managment-apis-overview).

---

**D: Quanti record è possibile scaricare dal portale di Azure?**

**R:** Dal portale di Azure è possibile scaricare fino a 120 KB di record. I record vengono ordinati in base ai *più recenti* e, per impostazione predefinita, vengono visualizzati 120 KB dei record più recenti. 

---

**D: Su quanti record è possibile eseguire query tramite le API delle attività?**

**R:** Le query possono essere eseguite su un numero massimo di 1 milione di record (se non si usa l'operatore TOP, che ordina i record in base al più recente). Se si usa l'operatore TOP, è possibile eseguire query su un massimo di 500 KB di record. [Qui](active-directory-reporting-api-getting-started.md) è possibile trovare le query di esempio su come usare l'API.

---

**D: Come ottenere una licenza Premium?**

**R:** Per la risposta a questa domanda, vedere [Introduzione ad Azure Active Directory Premium](active-directory-get-started-premium.md).

---

**D: In quanto tempo è possibile visualizzare le attività dopo aver acquistato una licenza Premium?**

**R:** Se si dispone già di dati sulle attività come licenza gratuita, è possibile visualizzare questi dati. Se non si dispone di dati, saranno necessari uno o due giorni.

---

**D: È possibile visualizzare i dati del mese precedente dopo avere acquistato una licenza Azure AD Premium?**

**R:**: Se di recente si è passati alla versione Premium (anche di valutazione), inizialmente è possibile visualizzare i dati fino a 7 giorni. Quando i dati si accumulano, verranno visualizzati fino a 30 giorni.

 
---


