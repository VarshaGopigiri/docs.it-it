---
title: Tipi di vincoli
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b6b246e6-1130-4698-9625-c5c42abcbfed
caps.latest.revision: "9"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 516733490dba459f452727d29320a366208b55fe
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/22/2017
---
# <a name="constraint-types"></a>Tipi di vincoli
In questo esempio vengono illustrate due modalità diverse per applicare vincoli a un flusso di lavoro: uno dall'interno dell'attività (compilazione) e un altro dall'esterno (criteri). In questo scenario, un autore di attività (di una società di software di terze parti) desidera convalidare la relazione tra due argomenti. In questo caso, il costo deve essere minore o uguale al prezzo. Si tratta di un vincolo di compilazione di convalida generale.  
  
 Il proprietario di un negozio desidera aggiungere alcune convalide a questa attività generica. In tal caso, desidera che la maggior parte dei prodotti abbia un prezzo pari ad almeno $9.99. Pertanto, usa un vincolo di criteri che si trova nella parte superiore dell'attività `CreateProduct`.  
  
 Nell'esempio:  
  
 L'autore di attività (compilazione) deve:  
  
-   Creare un vincolo (`PriceGreaterThanCost`), ovvero il punto in cui far risiedere l'intera logica di convalida.  
  
-   Eseguire l'override del metodo `System.Activities.CodeActivity.OnGetConstraints()` e aggiungere il vincolo (`PriceGreaterThanCost`) ai vincoli <xref:System.Collections.IList>.  
  
 L'autore del flusso di lavoro (criteri) deve:  
  
-   Creare un flusso di lavoro con un'istanza dell'attività da convalidare (`CreateProduct`).  
  
-   Creare un vincolo (`MaxPrice`),  
  
-   Creare un'istanza <xref:System.Activities.Validation.ValidationSettings> (`validationSettings`) e aggiungere il vincolo (`MaxPrice`) alla raccolta `AdditionalConstraints`. A questo punto l'autore del flusso di lavoro può aggiungere vincoli di criteri a qualsiasi attività, ad esempio Sequence o Parallel.  
  
-   Chiamare il metodo <xref:System.Activities.Validation.ActivityValidationServices.Validate%2A>, che restituisce una raccolta <xref:System.Activities.Validation.ValidationResults> di oggetti <xref:System.Activities.Validation.ValidationError>.  
  
-   (Facoltativo) Stampare gli oggetti <xref:System.Activities.Validation.ValidationError>.  
  
### <a name="to-set-up-build-and-run-the-sample"></a>Per impostare, compilare ed eseguire l'esempio  
  
1.  Aprire la soluzione di esempio ConstraintTypes.sln in [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)].  
  
2.  Compilare ed eseguire la soluzione.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer. Verificare la directory seguente (impostazione predefinita) prima di continuare.  
>   
>  `<InstallDrive>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation (WCF) e Windows Workflow Foundation (WF) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi di [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)] . Questo esempio si trova nella directory seguente.  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WF\Scenario\Validation\ConstraintLibrary`