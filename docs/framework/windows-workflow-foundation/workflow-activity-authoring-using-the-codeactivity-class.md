---
title: "Creazione di attività del flusso di lavoro tramite la classe CodeActivity"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: cfe315c1-f86d-43ec-b9ce-2f8c469b1106
caps.latest.revision: "11"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 2daec260c1224cd81280c6bf699b70efc2072588
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/22/2017
---
# <a name="workflow-activity-authoring-using-the-codeactivity-class"></a>Creazione di attività del flusso di lavoro tramite la classe CodeActivity
Le attività create ereditando dall'oggetto <xref:System.Activities.CodeActivity> possono implementare il comportamento imperativo di base eseguendo l'override del metodo <xref:System.Activities.CodeActivity.Execute%2A>.  
  
## <a name="using-codeactivitycontext"></a>Uso di CodeActivityContext  
 L'accesso a funzionalità dell'esecuzione del flusso di lavoro può essere eseguito dall'interno del metodo <xref:System.Activities.CodeActivity.Execute%2A> tramite i membri del parametro `context`, di tipo <xref:System.Activities.CodeActivityContext>. Tra le funzionalità disponibili tramite l'oggetto <xref:System.Activities.CodeActivityContext> sono incluse le seguenti:  
  
-   Recupero e impostazione di valori di variabili e di argomenti.  
  
-   Funzionalità di rilevamento personalizzate tramite <xref:System.Activities.CodeActivityContext.Track%2A>.  
  
-   Accesso alle proprietà di esecuzione dell'attività tramite il metodo <xref:System.Activities.CodeActivityContext.GetProperty%2A>.  
  
#### <a name="to-create-a-custom-activity-that-inherits-from-codeactivity"></a>Per creare un'attività personalizzata che eredita da CodeActivity  
  
1.  Aprire [!INCLUDE[vs2010](../../../includes/vs2010-md.md)].  
  
2.  Selezionare **File**, **nuova**e quindi **progetto**. Selezionare **Workflow 4.0** in **Visual c#** nel **tipi di progetto** window e selezionare il **v2010** nodo. Selezionare **libreria attività** nel **modelli** finestra. Assegnare al nuovo progetto il nome HelloActivity.  
  
3.  Fare doppio clic su Activity1 nel progetto HelloActivity e selezionare **eliminare**.  
  
4.  Fare clic sul progetto HelloActivity e selezionare **Aggiungi** e quindi **classe**. Assegnare alla nuova classe il nome HelloActivity.cs.  
  
5.  Nel file HelloActivity.cs aggiungere le seguenti istruzioni `using`.  
  
    ```csharp  
    using System.Activities;  
    using System.Activities.Statements;  
    ```  
  
6.  Assicurarsi che la nuova classe erediti dall'oggetto <xref:System.Activities.CodeActivity> aggiungendo una classe base alla dichiarazione di classe.  
  
    ```csharp  
    class HelloActivity : CodeActivity  
    ```  
  
7.  Aggiungere la funzionalità alla classe aggiungendo un metodo <xref:System.Activities.CodeActivity.Execute%2A>.  
  
    ```csharp  
    protected override void Execute(CodeActivityContext context)  
    {  
        Console.WriteLine("Hello World!");  
    }  
    ```  
  
8.  Usare l'oggetto <xref:System.Activities.CodeActivityContext> per creare un record di rilevamento.  
  
    ```csharp  
    protected override void Execute(CodeActivityContext context)  
    {  
        Console.WriteLine("Hello World!");  
        CustomTrackingRecord record = new CustomTrackingRecord("MyRecord");  
        record.Data.Add(new KeyValuePair<String, Object>("ExecutionTime", DateTime.Now));  
        context.Track(record);  
    }  
    ```
