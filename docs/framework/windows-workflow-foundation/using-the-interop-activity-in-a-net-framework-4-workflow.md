---
title: "Utilizzo dell'attività di interoperabilità in un flusso di lavoro di .NET Framework 4"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 9bb747f0-eb33-4f70-84cd-317382372dcd
caps.latest.revision: "20"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 0a02d6dbc7c6f6583a174bd10853d8c8070ac273
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/22/2017
---
# <a name="using-the-interop-activity-in-a-net-framework-4-workflow"></a>Utilizzo dell'attività di interoperabilità in un flusso di lavoro di .NET Framework 4
Le attività create tramite [!INCLUDE[vstecwinfx](../../../includes/vstecwinfx-md.md)] o [!INCLUDE[netfx35_short](../../../includes/netfx35-short-md.md)] possono essere usate nel flusso di lavoro di [!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)] mediante l'attività <xref:System.Activities.Statements.Interop>. In questo argomento viene fornita una panoramica sull'utilizzo dell'attività <xref:System.Activities.Statements.Interop>.  
  
> [!NOTE]
>  Il <xref:System.Activities.Statements.Interop> attività non viene visualizzato nella casella degli strumenti della finestra di progettazione del flusso di lavoro a meno che non dispone di progetto del flusso di lavoro relativo **Framework di destinazione** impostazione **.Net Framework 4** o versione successiva.  
  
## <a name="using-the-interop-activity-in-net-framework-45-workflows"></a>Utilizzo dell'attività di interoperabilità nei flussi di lavoro di .NET Framework 4.5  
 In questo argomento viene creata una libreria di attività di [!INCLUDE[netfx35_short](../../../includes/netfx35-short-md.md)] contenente un'attività `DiscountCalculator`. `DiscountCalculator` consente di calcolare uno sconto in base a un importo di acquisto ed è costituita da un oggetto <xref:System.Workflow.Activities.SequenceActivity> contenente un oggetto <xref:System.Workflow.Activities.PolicyActivity>.  
  
> [!NOTE]
>  L'attività di [!INCLUDE[netfx35_short](../../../includes/netfx35-short-md.md)] creata in questo argomento usa un oggetto <xref:System.Workflow.Activities.PolicyActivity> per implementare la logica dell'attività. Non è necessario usare un'attività [!INCLUDE[netfx35_short](../../../includes/netfx35-short-md.md)] personalizzata o l'attività <xref:System.Activities.Statements.Interop> per sfruttare le regole in un flusso di lavoro di [!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)]. Per un esempio di utilizzo di regole in un [!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)] flusso di lavoro senza utilizzare il <xref:System.Activities.Statements.Interop> attività, vedere il [attività Policy in .NET Framework 4.5](../../../docs/framework/windows-workflow-foundation/samples/policy-activity-in-net-framework-4-5.md) esempio.  
  
#### <a name="to-create-the-net-framework-35-activity-library-project"></a>Per creare il progetto della libreria di attività di .NET Framework 3.5  
  
1.  Aprire [!INCLUDE[vs_current_long](../../../includes/vs-current-long-md.md)] e selezionare **New** e quindi **progetto...** dal **File** menu.  
  
2.  Espandere il **altri tipi di progetto** nodo il **modelli installati** riquadro e selezionare **soluzioni di Visual Studio**.  
  
3.  Selezionare **soluzione vuota** dal **soluzioni di Visual Studio** elenco. Tipo `PolicyInteropDemo` nel **nome** casella e fare clic su **OK**.  
  
4.  Fare doppio clic su **PolicyInteropDemo** in **Esplora** e selezionare **Aggiungi** e quindi **nuovo progetto...** .  
  
    > [!TIP]
    >  Se il **Esplora** finestra non è visibile, selezionare **Esplora** dal **vista** menu.  
  
5.  Nel **modelli installati** elenco, selezionare **Visual c#** e quindi **flusso di lavoro**. Selezionare **.NET Framework 3.5** dall'elenco a discesa versione .NET Framework e quindi selezionare **Workflow Activity Library** dal **modelli** elenco.  
  
6.  Tipo `PolicyActivityLibrary` nel **nome** casella e fare clic su **OK**.  
  
7.  Fare doppio clic su **Activity1. cs** in **Esplora** e selezionare **eliminare**. Per confermare scegliere **OK** .  
  
#### <a name="to-create-the-discountcalculator-activity"></a>Per creare l'attività DiscountCalculator  
  
1.  Fare doppio clic su **PolicyActivityLibrary** in **Esplora** e selezionare **Aggiungi** e quindi **attività...** .  
  
2.  Selezionare **attività (con separazione del codice)** dal **elementi di Visual c#** elenco. Tipo `DiscountCalculator` nel **nome** casella e fare clic su **OK**.  
  
3.  Fare doppio clic su **Discountcalculator** in **Esplora** e selezionare **Visualizza codice**.  
  
4.  Aggiungere le tre seguenti proprietà alla classe `DiscountCalculator`.  
  
    ```csharp  
    public partial class DiscountCalculator : SequenceActivity  
    {  
        public double Subtotal { get; set; }  
        public double DiscountPercent { get; set; }  
        public double Total { get; set; }  
    }  
    ```  
  
5.  Fare doppio clic su **Discountcalculator** in **Esplora** e selezionare **Visualizza finestra di progettazione**.  
  
6.  Trascinare un **criteri** attività dal **Windows Workflow v 3.0** sezione il **della casella degli strumenti** e rilasciarlo nel **DiscountCalculator** attività .  
  
    > [!TIP]
    >  Se il **della casella degli strumenti** finestra non è visibile, selezionare **della casella degli strumenti** dal **vista** menu.  
  
#### <a name="to-configure-the-rules"></a>Per configurare le regole  
  
1.  Fare clic su appena aggiunta **criteri** attività per selezionarlo, se non è già selezionato.  
  
2.  Fare clic su di **RuleSetReference** proprietà il **proprietà** finestra per selezionarla e fare clic sul pulsante con i puntini di sospensione a destra della proprietà.  
  
    > [!TIP]
    >  Se il **proprietà** finestra non è visibile, scegliere **finestra proprietà** dal **vista** menu.  
  
3.  Selezionare **fare clic su nuovo...** .  
  
4.  Fare clic su **Aggiungi regola**.  
  
5.  Digitare l'espressione seguente nella **condizione** casella.  
  
    ```  
    this.Subtotal >= 50 && this.Subtotal < 100  
    ```  
  
6.  Digitare l'espressione seguente nella **azioni Then** casella.  
  
    ```  
    this.DiscountPercent = 0.075  
    ```  
  
7.  Fare clic su **Aggiungi regola**.  
  
8.  Digitare l'espressione seguente nella **condizione** casella.  
  
    ```  
    this.Subtotal >= 100  
    ```  
  
9. Digitare l'espressione seguente nella **azioni Then** casella.  
  
    ```  
    this.DiscountPercent = 0.15  
    ```  
  
10. Fare clic su **Aggiungi regola**.  
  
11. Digitare l'espressione seguente nella **condizione** casella.  
  
    ```  
    this.DiscountPercent > 0  
    ```  
  
12. Digitare l'espressione seguente nella **azioni Then** casella.  
  
    ```  
    this.Total = this.Subtotal - this.Subtotal * this.DiscountPercent  
    ```  
  
13. Digitare l'espressione seguente nella **azioni Else** casella.  
  
    ```  
    this.Total = this.Subtotal  
    ```  
  
14. Fare clic su **OK** per chiudere la **Editor Set di regole** la finestra di dialogo.  
  
15. Verificare che il nuovo <xref:System.Workflow.Activities.Rules.RuleSet> è selezionata nel **nome** elenco e fare clic su **OK**.  
  
16. Per compilare la soluzione, premere CTRL+MAIUSC+B.  
  
 Le regole aggiunte all'attività `DiscountCalculator` in questa procedura vengono mostrate nell'esempio di codice seguente.  
  
```  
Rule1: IF this.Subtotal >= 50 && this.Subtotal < 100   
       THEN this.DiscountPercent = 0.075   
  
Rule2: IF this. Subtotal >= 100   
       THEN this.DiscountPercent = 0.15   
  
Rule3: IF this.DiscountPercent > 0   
       THEN this.Total = this.Subtotal - this.Subtotal * this.DiscountPercent   
       ELSE this.Total = this.Subtotal  
```  
  
 Quando l'oggetto <xref:System.Workflow.Activities.PolicyActivity> viene eseguito, queste tre regole valutano e modificano i valori delle proprietà `Subtotal`, `DiscountPercent` e `Total` dell'attività `DiscountCalculator` per calcolare lo sconto desiderato.  
  
## <a name="using-the-discountcalculator-activity-with-the-interop-activity"></a>Utilizzo dell'attività DiscountCalculator con l'attività di interoperabilità  
 Per usare l'attività `DiscountCalculator` in un flusso di lavoro di [!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)], viene usata l'attività <xref:System.Activities.Statements.Interop>. Contenuto della sezione vengono creati due flussi di lavoro (in uno viene usato il codice e nell'altro la relativa utilità di progettazione) che illustrano come usare l'attività <xref:System.Activities.Statements.Interop> con l'attività `DiscountCalculator`. In entrambi i flussi di lavoro viene usata la stessa applicazione host.  
  
#### <a name="to-create-the-host-application"></a>Per creare l'applicazione host  
  
1.  Fare doppio clic su **PolicyInteropDemo** in **Esplora** e selezionare **Aggiungi**e quindi **nuovo progetto...** .  
  
2.  Verificare che **.NET Framework 4.5** sia selezionata nell'elenco a discesa versione di .NET Framework e selezionare **applicazione Console flusso di lavoro** dal **elementi di Visual c#** elenco.  
  
3.  Tipo `PolicyInteropHost` nel **nome** casella e fare clic su **OK**.  
  
4.  Fare doppio clic su **PolicyInteropHost** in **Esplora** e selezionare **proprietà**.  
  
5.  Nel **framework di destinazione** elenco a discesa elenco, modificare la selezione da **.NET Framework 4 Client Profile** a **.NET Framework 4.5**. Fare clic su **Sì** per confermare.  
  
6.  Fare doppio clic su **PolicyInteropHost** in **Esplora** e selezionare **Aggiungi riferimento...** .  
  
7.  Selezionare **PolicyActivityLibrary** dal **progetti** scheda e fare clic su **OK**.  
  
8.  Fare doppio clic su **PolicyInteropHost** in **Esplora** e selezionare **Aggiungi riferimento...** .  
  
9. Selezionare **System.Workflow.Activities**, **ComponentModel**e quindi **System.Workflow.Runtime** dal **.NET**scheda e fare clic su **OK**.  
  
10. Fare doppio clic su **PolicyInteropHost** in **Esplora** e selezionare **imposta come progetto di avvio**.  
  
11. Per compilare la soluzione, premere CTRL+MAIUSC+B.  
  
### <a name="using-the-interop-activity-in-code"></a>Utilizzo dell'attività di interoperabilità nel codice  
 In questo esempio viene creata una definizione di flusso di lavoro tramite il codice contenente le attività <xref:System.Activities.Statements.Interop> e `DiscountCalculator`. Questo flusso di lavoro viene richiamato usando l'oggetto <xref:System.Activities.WorkflowInvoker> e i risultati della valutazione della regola vengono scritti nella console tramite un'attività <xref:System.Activities.Statements.WriteLine>.  
  
##### <a name="to-use-the-interop-activity-in-code"></a>Per usare l'attività di interoperabilità nel codice  
  
1.  Fare doppio clic su **Program.cs** in **Esplora** e selezionare **Visualizza codice**.  
  
2.  Aggiungere la seguente istruzione `using` all'inizio del file.  
  
    ```csharp  
    using PolicyActivityLibrary;  
    ```  
  
3.  Rimuovere il contenuto del metodo `Main` e sostituirlo con il codice riportato di seguito.  
  
    ```csharp  
    static void Main(string[] args)  
    {  
        CalculateDiscountUsingCodeWorkflow();  
    }  
    ```  
  
4.  Creare un nuovo metodo nella classe `Program` denominato `CalculateDiscountUsingCodeWorkflow` contenente il codice seguente.  
  
    ```csharp  
    static void CalculateDiscountUsingCodeWorkflow()  
    {  
        Variable<double> Subtotal = new Variable<double>  
        {  
            Default = 75.99,  
            Name = "Subtotal"  
        };  
  
        Variable<double> DiscountPercent = new Variable<double>  
        {  
            Name = "DiscountPercent"  
        };  
  
        Variable<double> Total = new Variable<double>  
        {  
            Name = "Total"  
        };  
  
        Activity wf = new Sequence  
        {  
            Variables = { Subtotal, DiscountPercent, Total },  
            Activities =   
            {  
                new Interop  
                {  
                    ActivityType = typeof(DiscountCalculator),  
                    ActivityProperties =   
                    {  
                        { "Subtotal", new InArgument<double>(Subtotal) },  
                        { "DiscountPercentOut", new OutArgument<double>(DiscountPercent) },  
                        { "TotalOut", new OutArgument<double>(Total) }  
                    }  
                },  
                new WriteLine  
                {  
                    Text =  new InArgument<string>(env =>   
                        string.Format("Subtotal: {0:C}, Discount {1}%, Total {2:C}",   
                        Subtotal.Get(env), DiscountPercent.Get(env) * 100, Total.Get(env)))  
                }  
            }  
        };  
  
        WorkflowInvoker.Invoke(wf);  
    }  
    ```  
  
    > [!NOTE]
    >  Le proprietà `Subtotal`, `DiscountPercent` e `Total` dell'attività `DiscountCalculator` vengono rilevate come argomenti dell'attività <xref:System.Activities.Statements.Interop> e associate a variabili del flusso di lavoro locali nella raccolta <xref:System.Activities.Statements.Interop> dell'attività <xref:System.Activities.Statements.Interop.ActivityProperties%2A>. `Subtotal` viene aggiunto come argomento di <xref:System.Activities.ArgumentDirection.In> in quanto i dati di `Subtotal` fluiscono nell'attività <xref:System.Activities.Statements.Interop>; `DiscountPercent` e `Total` vengono aggiunti come argomenti di <xref:System.Activities.ArgumentDirection.Out> in quanto i relativi dati escono dall'attività <xref:System.Activities.Statements.Interop>. Si noti che i due argomenti <xref:System.Activities.ArgumentDirection.Out> vengono aggiunti con i nomi `DiscountPercentOut` e `TotalOut` per indicare che rappresentano gli argomenti <xref:System.Activities.ArgumentDirection.Out>. Il tipo `DiscountCalculator` viene specificato come proprietà <xref:System.Activities.Statements.Interop> dell'attività <xref:System.Activities.Statements.Interop.ActivityType%2A>.  
  
5.  Premere CTRL+F5 per compilare ed eseguire l'applicazione. Sostituire i diversi valori per il valore `Subtotal` al fine di testare i numerosi livelli di sconto forniti dall'attività `DiscountCalculator`.  
  
    ```csharp  
    Variable<double> Subtotal = new Variable<double>  
    {  
        Default = 75.99, // Change this value.  
        Name = "Subtotal"  
    };  
    ```  
  
### <a name="using-the-interop-activity-in-the-workflow-designer"></a>Utilizzo dell'attività di interoperabilità nell'utilità di progettazione del flusso di lavoro  
 In questo esempio viene creato un flusso di lavoro tramite l'utilità di progettazione del flusso di lavoro. Questo flusso di lavoro dispone della stessa funzionalità descritta nell'esempio precedente, tuttavia anziché usare un'attività <xref:System.Activities.Statements.WriteLine> per visualizzare lo sconto, l'applicazione host recupera e visualizza le informazioni sullo sconto quando il flusso di lavoro viene completato. Inoltre, invece di usare le variabili del flusso di lavoro locale per contenere i dati, gli argomenti vengono creati nell'utilità di progettazione del flusso di lavoro e i valori vengono passati dall'host quando il flusso di lavoro viene richiamato.  
  
##### <a name="to-host-the-policyactivity-using-a-workflow-designer-created-workflow"></a>Per ospitare PolicyActivity usando un flusso di lavoro creato tramite la relativa utilità di progettazione  
  
1.  Fare doppio clic su **Workflow1** in **Esplora** e selezionare **eliminare**. Per confermare scegliere **OK** .  
  
2.  Fare doppio clic su **PolicyInteropHost** in **Esplora** e selezionare **Aggiungi**, **nuovo elemento...** .  
  
3.  Espandere il **elementi di Visual c#** nodo e selezionare **flusso di lavoro**. Selezionare **attività** dal **elementi di Visual c#** elenco.  
  
4.  Tipo `DiscountWorkflow` nel **nome** casella e fare clic su **Aggiungi**.  
  
5.  Fare clic su di **argomenti** pulsante sul lato inferiore sinistro della finestra di progettazione del flusso di lavoro per visualizzare il **argomenti** riquadro.  
  
6.  Fare clic su **Crea argomento**.  
  
7.  Tipo `Subtotal` nel **nome** , quindi selezionare **In** dal **direzione** elenco a discesa, selezionare **doppie** dal **Tipo di argomento** elenco a discesa, quindi premere INVIO per salvare l'argomento.  
  
    > [!NOTE]
    >  Se **doppie** non si trova nel **tipo di argomento** elenco a discesa, seleziona **Cerca tipi...** , tipo `System.Double` nel **nome del tipo** casella e fare clic su **OK**.  
  
8.  Fare clic su **Crea argomento**.  
  
9. Tipo `DiscountPercent` nel **nome** , quindi selezionare **Out** dal **direzione** elenco a discesa, selezionare **doppie** dal **Tipo di argomento** elenco a discesa, quindi premere INVIO per salvare l'argomento.  
  
10. Fare clic su **Crea argomento**.  
  
11. Tipo `Total` nel **nome** , quindi selezionare **Out** dal **direzione** elenco a discesa, selezionare **doppie** dal **Tipo di argomento** elenco a discesa, quindi premere INVIO per salvare l'argomento.  
  
12. Fare clic su di **argomenti** pulsante sul lato inferiore sinistro della finestra di progettazione del flusso di lavoro per chiudere la **argomenti** riquadro.  
  
13. Trascinare un **sequenza** attività dal **flusso di controllo** sezione il **della casella degli strumenti** e rilasciarlo nell'area di progettazione del flusso di lavoro.  
  
14. Trascinare un **interoperabilità** attività dal **migrazione** sezione il **della casella degli strumenti** e rilasciarlo nel **sequenza** attività.  
  
15. Fare clic sul **interoperabilità** attività di **fare clic per cercare...** etichetta, digitare **DiscountCalculator** nel **nome del tipo** casella e fare clic su **OK**.  
  
    > [!NOTE]
    >  Quando l'attività <xref:System.Activities.Statements.Interop> viene aggiunta al flusso di lavoro e il tipo `DiscountCalculator` viene specificato come la relativa proprietà <xref:System.Activities.Statements.Interop.ActivityType%2A>, l'attività <xref:System.Activities.Statements.Interop> espone tre argomenti <xref:System.Activities.ArgumentDirection.In> e tre argomenti <xref:System.Activities.ArgumentDirection.Out> che rappresentano le tre proprietà pubbliche dell'attività `DiscountCalculator`. Il <xref:System.Activities.ArgumentDirection.In> argomenti con lo stesso nome delle tre proprietà pubbliche e i tre <xref:System.Activities.ArgumentDirection.Out> argomenti hanno gli stessi nomi con **Out** aggiunto al nome della proprietà. Nei passaggi seguenti gli argomenti del flusso di lavoro creati in precedenza vengono associati agli argomenti dell'attività <xref:System.Activities.Statements.Interop>.  
  
16. Tipo `DiscountPercent` nel **immettere un'espressione VB** casella a destra del **DiscountPercentOut** proprietà e premere TAB.  
  
17. Tipo `Subtotal` nel **immettere un'espressione VB** casella a destra del **Subtotal** proprietà e premere TAB.  
  
18. Tipo `Total` nel **immettere un'espressione VB** casella a destra del **TotalOut** proprietà e premere TAB.  
  
19. Fare doppio clic su **Program.cs** in **Esplora** e selezionare **Visualizza codice**.  
  
20. Aggiungere la seguente istruzione `using` all'inizio del file.  
  
    ```csharp  
    using System.Collections.Generic;  
    ```  
  
21. Impostare come commento la chiamata al metodo `CalculateDiscountInCode` nel metodo `Main` e aggiungere il codice seguente.  
  
    > [!NOTE]
    >  Se non è stata seguita la procedura precedente e il codice `Main` predefinito è presente, sostituire il contenuto di `Main` con il codice seguente.  
  
    ```csharp  
    static void Main(string[] args)  
    {  
        CalculateDiscountUsingDesignerWorkflow();  
        //CalculateDiscountUsingCodeWorkflow();  
    }  
    ```  
  
22. Creare un nuovo metodo nella classe `Program` denominato `CalculateDiscountUsingDesignerWorkflow` contenente il codice seguente.  
  
    ```csharp  
    static void CalculateDiscountUsingDesignerWorkflow()  
    {  
        double SubtotalValue = 125.99;  
        Dictionary<string, object> wfargs = new Dictionary<string, object>  
        {  
            {"Subtotal", SubtotalValue}  
        };  
  
        Activity wf = new DiscountWorkflow();  
  
        IDictionary<string, object> outputs =  
            WorkflowInvoker.Invoke(wf, wfargs);  
  
        Console.WriteLine("Subtotal: {0:C}, Discount {1}%, Total {2:C}",  
            SubtotalValue, (double)outputs["DiscountPercent"] * 100,  
            outputs["Total"]);  
    }  
    ```  
  
23. Premere CTRL+F5 per compilare ed eseguire l'applicazione. Per specificare un importo `Subtotal` diverso, modificare il valore di `SubtotalValue` nel codice seguente.  
  
    ```csharp  
    double SubtotalValue = 125.99; // Change this value.  
    ```  
  
## <a name="rules-features-overview"></a>Panoramica sulle funzionalità delle regole  
 Il motore di regole in [!INCLUDE[wf1](../../../includes/wf1-md.md)] facilita l'elaborazione di regole basata sulla priorità con supporto del concatenamento diretto. Le regole possono essere valutate per un singolo elemento o per gli elementi di una raccolta. Per una panoramica sulle regole e per informazioni sulla funzionalità di regole specifiche, fare riferimento alla tabella seguente.  
  
|Funzionalità delle regole|Documentazione|  
|-------------------|-------------------|  
|Panoramica sulle regole|[Introduzione al motore regole di Windows Workflow Foundation](http://go.microsoft.com/fwlink/?LinkID=152836)|  
|RuleSet|[Uso di RuleSet in flussi di lavoro](http://go.microsoft.com/fwlink/?LinkId=178516) e<xref:System.Workflow.Activities.Rules.RuleSet>|  
|Valutazione delle regole|[Valutazione delle regole di RuleSet](http://go.microsoft.com/fwlink/?LinkId=178517)|  
|Concatenamento di regole|[Controllo del concatenamento diretto](http://go.microsoft.com/fwlink/?LinkId=178518) e [concatenamento diretto di regole](http://go.microsoft.com/fwlink/?LinkId=178519)|  
|Elaborazione di raccolte nelle regole|[Elaborazione di raccolte nelle regole](http://go.microsoft.com/fwlink/?LinkId=178520)|  
|Utilizzo dell'attività PolicyActivity|[Utilizzo dell'attività PolicyActivity](http://go.microsoft.com/fwlink/?LinkId=178521) e<xref:System.Workflow.Activities.PolicyActivity>|  
  
 I flussi di lavoro creati in [!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)] non usano tutte le funzionalità delle regole fornite da [!INCLUDE[wf1](../../../includes/wf1-md.md)], ad esempio le condizioni di attività dichiarative e le attività condizionali quali <xref:System.Workflow.Activities.ConditionedActivityGroup> e <xref:System.Workflow.Activities.ReplicatorActivity>. Se necessario, questa funzionalità è disponibile per i flussi di lavoro creati tramite [!INCLUDE[vstecwinfx](../../../includes/vstecwinfx-md.md)] e [!INCLUDE[netfx35_short](../../../includes/netfx35-short-md.md)]. [!INCLUDE[crdefault](../../../includes/crdefault-md.md)][Materiale sussidiario sulla migrazione](../../../docs/framework/windows-workflow-foundation/migration-guidance.md).
