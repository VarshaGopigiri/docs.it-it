---
title: Esempio di compensazione personalizzata
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 385920da-9284-44bf-9fe9-0d87c7478ec5
caps.latest.revision: "13"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 2bc76267cf4b3fe5f4e792ee185733e51185872f
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/22/2017
---
# <a name="custom-compensation-sample"></a>Esempio di compensazione personalizzata
In questo esempio viene illustrato come usare <xref:System.Activities.Statements.CompensableActivity> e il relativo gestore di compensazione per definire la logica di compensazione personalizzata. Lo scenario modellato in questo esempio è una Agenzia di noleggio furgoni.  
  
## <a name="sample-details"></a>Dettagli dell'esempio  
 Di seguito sono riportati i passaggi simulati:  
  
1.  L'utente richiede preventivi per il noleggio di furgoni per una data specificata.  
  
2.  Vengono contattate tre società di noleggio furgoni e vengono forniti tre preventivi.  
  
3.  L'utente sceglie un preventivo e procede all'ordine tramite carta di credito.  
  
4.  Gli altri due preventivi vengono annullati dall'applicazione.  
  
5.  Tramite l'applicazione viene addebitata una commissione di servizio che non è risarcibile, per i clienti privi di un conto premium, se l'annullamento avviene entro un massimo di 10 giorni antecedenti la data di prenotazione.  
  
6.  Tramite l'applicazione viene addebitata la tariffa di noleggio del furgone.  
  
7.  L'applicazione attende fino alla data di prenotazione o fino a quando il cliente decide di annullare la prenotazione, a seconda dell'evento che si verifica per primo.  
  
8.  Se il cliente annulla la prenotazione, viene eseguita la logica di compensazione personalizzata <xref:System.Activities.Statements.CompensableActivity.CompensationHandler%2A> in base alla logica seguente:  
  
    1.  Se il cliente non dispone di un conto "premium" e mancano meno di 10 giorni alla data di prenotazione, la commissione di servizio viene comunque addebitata. In caso contrario, la commissione di servizio viene rimborsata dall'applicazione.  
  
    2.  Il resto delle attività compensabili (ordine del furgone + tariffa di ordine del furgone) viene eseguito sulla base della logica di compensazione predefinita che consiste nel compensare in ordine inverso di esecuzione.  
  
#### <a name="to-set-up-build-and-run-the-sample"></a>Per impostare, compilare ed eseguire l'esempio  
  
1.  In [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] aprire il file della soluzione CustomCompensation.sln. Si trova nella directory \WF\Basic\Compensation\CustomCompensation.  
  
2.  Per compilare la soluzione, premere CTRL+MAIUSC+B.  
  
3.  Premere CTRL+F5 per eseguire l'applicazione.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer. Verificare la directory seguente (impostazione predefinita) prima di continuare.  
>   
>  `<InstallDrive>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation (WCF) e Windows Workflow Foundation (WF) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi di [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)] . Questo esempio si trova nella directory seguente.  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WF\Basic\Compensation\CustomCompensation`