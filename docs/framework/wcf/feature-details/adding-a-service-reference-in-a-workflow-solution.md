---
title: Aggiunta di un riferimento al servizio in una soluzione del flusso di lavoro
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 83574cf3-9803-49bc-837f-432936dc9c76
caps.latest.revision: "5"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: ee974ee5a9f4564b0e44256bc4773f9898d89fc6
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/22/2017
---
# <a name="adding-a-service-reference-in-a-workflow-solution"></a>Aggiunta di un riferimento al servizio in una soluzione del flusso di lavoro
L'aggiunta di un riferimento al servizio in un'applicazione flusso di lavoro è leggermente differente da quella in un'applicazione WCF normale. Quando si seleziona Aggiungi riferimento al servizio e si specifica l'URL del servizio, i metadati vengono scaricati e le attività personalizzate vengono generate per consentire la chiamata al servizio WCF o al servizio del flusso di lavoro WCF a cui è stato aggiunto un riferimento. Dopo avere aggiunto un riferimento al servizio, ricompilare la soluzione per compilare le attività generate che verranno visualizzate nella casella degli strumenti di Progettazione flussi di lavoro. Notare tuttavia che l'operazione viene eseguita solo se si aggiunge un riferimento al servizio all'interno di una soluzione del flusso di lavoro. Il cast di web riportato di seguito viene illustrato come aggiungere un riferimento al servizio in altri tipi di progetti: [chiama un servizio WCF da un flusso di lavoro in un progetto Web](http://go.microsoft.com/fwlink/?LinkId=207725).  
  
 L'aggiunta di due o più riferimenti ai servizi contenenti lo stesso nome di operazione causa un problema. Le attività generate chiameranno solo la prima operazione del servizio. Per ovviare a questo problema rinominare le operazioni del servizio in modo da renderle diverse o modificano il nome di configurazione dell'endpoint all'interno di ogni attività generata.  
  
## <a name="see-also"></a>Vedere anche  
 [Servizi flusso di lavoro](../../../../docs/framework/wcf/feature-details/workflow-services.md)  
 [Procedura: Creare un servizio flusso di lavoro che chiama un altro servizio flusso di lavoro](../../../../docs/framework/wcf/feature-details/how-to-create-a-workflow-service-that-calls-another-workflow-service.md)  
 [Chiamata di un servizio WCF da un flusso di lavoro in un progetto Web](http://go.microsoft.com/fwlink/?LinkId=207725)
