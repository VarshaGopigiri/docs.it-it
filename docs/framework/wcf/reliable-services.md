---
title: Servizi affidabili
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- WCF [WCF], reliable messaging
- Windows Communication Foundation [WCF], reliable messaging
- WCF [WCF], reliable sessions
- Windows Communication Foundation [WCF], reliable sessions
- service contracts [WCF], reliable services
ms.assetid: 07814ed0-0775-47f2-987b-d8134fdd5099
caps.latest.revision: "8"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 408801e28fec71f133c2dddd3f30b2509ab5896c
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/22/2017
---
# <a name="reliable-services"></a>Servizi affidabili
Code e sessioni affidabili rappresentano le funzionalità di [!INCLUDE[indigo1](../../../includes/indigo1-md.md)] per l'implementazione della messaggistica affidabile. In questo argomento vengono illustrate le funzionalità di messaggistica affidabile di [!INCLUDE[indigo2](../../../includes/indigo2-md.md)].  
  
 *Messaggistica affidabile* riguarda il modo in un'origine di messaggistica affidabile (chiamato il *origine*) trasferisce in modo affidabile i messaggi a una destinazione di messaggistica affidabile (chiamata di *destinazione*).  
  
 La messaggistica affidabile esegue le funzioni seguenti:  
  
-   Trasferisce le garanzie per i messaggi inviati da un'origine a una destinazione indipendentemente dagli errori di trasporto o di trasferimento dei messaggi.  
  
-   Separa l'una dall'altra l'origine e la destinazione. In questo modo viene fornito un errore e un recupero indipendente dell'origine e della destinazione, nonché un trasferimento e un recapito affidabile dei messaggi, anche quando l'origine o la destinazione non è disponibile.  
  
 La messaggistica affidabile comporta spesso il costo di una latenza elevata. *Latenza* è il tempo necessario per il messaggio raggiungere la destinazione dall'origine. In [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] vengono pertanto forniti i tipi seguenti di messaggistica affidabile:  
  
-   [Le sessioni affidabili](../../../docs/framework/wcf/feature-details/reliable-sessions.md), che offre il trasferimento affidabile senza il costo di latenza elevata.  
  
-   [Le code in WCF](../../../docs/framework/wcf/feature-details/queues-in-wcf.md), che offre sia trasferimento affidabile e la separazione tra l'origine e destinazione.  
  
## <a name="reliable-sessions"></a>Sessioni affidabili  
 Le sessioni affidabili forniscono un trasferimento affidabile end-to-end dei messaggi tra un'origine e una destinazione utilizzando il protocollo WS-Reliable Messaging, indipendentemente dal numero o dal tipo di intermediari che separano gli endpoint di messaggistica (origine e destinazione). In questo modo vengono inclusi tutti gli intermediari del trasporto che non utilizzano SOAP (ad esempio proxy HTTP) o gli intermediari che utilizzano SOAP (ad esempio bridge o router basati su SOAP) necessari per il flusso dei messaggi tra gli endpoint. Le sessioni affidabili utilizzano una finestra di trasferimento in memoria per mascherare gli errori a livello di messaggio SOAP e riattivare le connessioni in caso di errori di trasporto.  
  
 Le sessioni affidabili forniscono trasferimenti affidabili dei messaggi con una latenza bassa. Provvedono ai messaggi SOAP su qualsiasi proxy o intermediario, in modo equivalente a TCP per i pacchetti su bridge IP. [!INCLUDE[crabout](../../../includes/crabout-md.md)]le sessioni affidabili, vedere [le sessioni affidabili](../../../docs/framework/wcf/feature-details/reliable-sessions.md).  
  
### <a name="queues"></a>Code  
 Le code in [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] forniscono il trasferimento affidabile dei messaggi e la separazione tra le origini e le destinazioni al prezzo di una latenza elevata. La comunicazione in coda di [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] si basa su Accodamento messaggi (MSMQ).  
  
 MSMQ viene fornito con Windows come componente facoltativo. Il servizio MSMQ viene eseguito come un servizio di Windows. Acquisisce i messaggi da trasmettere in una coda di trasmissione per conto dell'origine e li recapita a una coda di destinazione. La coda di destinazione accetta i messaggi per conto della destinazione a cui verranno recapitati in seguito quando la destinazione richiederà i messaggi. I gestori MSMQ implementano un protocollo di trasferimento messaggi affidabile in modo che i messaggi non vadano persi durante la trasmissione. Il protocollo può essere nativo o un protocollo basato su SOAP denominato SRMP (SOAP Reliable Messagging Protocol).  
  
 La separazione, abbinata ai trasferimenti affidabili dei messaggi tra le code, consente alle applicazioni ad accoppiamento debole di comunicare in modo affidabile. A differenza delle sessioni affidabili, non è necessario che l'origine e la destinazione siano in esecuzione contemporaneamente. Questo consente implicitamente scenari in cui le code vengono di fatto utilizzate come un meccanismo di livellamento del carico nei casi in cui il tasso di produzione di messaggi dell'origine e il tasso di utilizzo di messaggi della destinazione non corrispondono. [!INCLUDE[crabout](../../../includes/crabout-md.md)]le code, vedere [code in WCF](../../../docs/framework/wcf/feature-details/queues-in-wcf.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Panoramica delle sessioni affidabili](../../../docs/framework/wcf/feature-details/reliable-sessions-overview.md)  
 [Accodamento in WCF](../../../docs/framework/wcf/feature-details/queuing-in-wcf.md)
