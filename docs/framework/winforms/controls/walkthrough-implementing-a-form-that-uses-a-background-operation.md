---
title: 'Procedura dettagliata: implementazione di un form che utilizza un''operazione in background'
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-winforms
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- threading [Windows Forms], forms
- BackgroundWorker component
- background tasks
- forms [Windows Forms], multithreading
- threading [Windows Forms], walkthroughs
- forms [Windows Forms], background operations
- threading [Windows Forms], background operations
- background operations
ms.assetid: 4691b796-9200-471a-89c3-ba4c7cc78c03
caps.latest.revision: "25"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: aaee6f1d650e6af57ab05ad56b5578e094ee50ef
ms.sourcegitcommit: c0dd436f6f8f44dc80dc43b07f6841a00b74b23f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/19/2018
---
# <a name="walkthrough-implementing-a-form-that-uses-a-background-operation"></a>Procedura dettagliata: implementazione di un form che utilizza un'operazione in background
Se si esegue un'operazione che richiederà molto tempo per completare, e per evitare l'interfaccia utente (UI) di rispondere o "blocco", è possibile utilizzare la <xref:System.ComponentModel.BackgroundWorker> classe per eseguire l'operazione in un altro thread.  
  
 Questa procedura dettagliata viene illustrato come utilizzare la <xref:System.ComponentModel.BackgroundWorker> classe per eseguire calcoli richiede molto tempo "in"background, mentre l'interfaccia utente rimane attiva.  Nel corso della procedura, un'applicazione calcola i numeri Fibonacci in modo asincrono. Sebbene il calcolo di un numero Fibonacci a molte cifre possa impiegare una notevole quantità di tempo, il thread principale dell'interfaccia utente non verrà interrotto da questa operazione e la capacità di risposta del modulo resterà inalterata durante il calcolo.  
  
 Le attività illustrate nella procedura dettagliata sono le seguenti:  
  
-   Creazione di un'applicazione basata su Windows  
  
-   Creazione di un <xref:System.ComponentModel.BackgroundWorker> del modulo  
  
-   Aggiunta dei gestori eventi asincroni  
  
-   Aggiunta dei report sullo stato di avanzamento e supporto per l'annullamento  
  
 Per il listato completo del codice utilizzato in questo esempio, vedere [Procedura: Implementare un modulo che utilizza un'operazione in background](../../../../docs/framework/winforms/controls/how-to-implement-a-form-that-uses-a-background-operation.md).  
  
> [!NOTE]
>  Le finestre di dialogo e i comandi di menu visualizzati potrebbero essere diversi da quelli descritti nella Guida a seconda delle impostazioni attive o dell'edizione del programma. Per modificare le impostazioni, scegliere **Importa/Esporta impostazioni** dal menu **Strumenti** . Per altre informazioni, vedere [Personalizzazione delle impostazioni di sviluppo in Visual Studio](http://msdn.microsoft.com/library/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
## <a name="creating-the-project"></a>Creazione del progetto  
 Il primo passaggio indica come creare il progetto e impostare il modulo.  
  
#### <a name="to-create-a-form-that-uses-a-background-operation"></a>Per creare un modulo che utilizza un'operazione in background  
  
1.  Creare un progetto di applicazione basata su Windows chiamato `BackgroundWorkerExample`. Per informazioni dettagliate, vedere [Procedura: creare un progetto di applicazione Windows](http://msdn.microsoft.com/library/b2f93fed-c635-4705-8d0e-cf079a264efa).  
  
2.  In **Esplora soluzioni** fare clic con il pulsante destro del mouse su **Form1** e scegliere **Rinomina** dal menu di scelta rapida. Modificare il nome file in `FibonacciCalculator`. Scegliere il pulsante **Sì** quando richiesto per rinominare tutti i riferimenti all'elemento di codice '`Form1`'.  
  
3.  Trascinare un <xref:System.Windows.Forms.NumericUpDown> controllo il **della casella degli strumenti** nel form. Impostare il <xref:System.Windows.Forms.NumericUpDown.Minimum%2A> proprietà `1` e <xref:System.Windows.Forms.NumericUpDown.Maximum%2A> proprietà `91`.  
  
4.  Aggiungere due <xref:System.Windows.Forms.Button> controlli al form.  
  
5.  Rinominare il primo <xref:System.Windows.Forms.Button> controllo `startAsyncButton` e impostare il <xref:System.Windows.Forms.Control.Text%2A> proprietà `Start Async`. Rinomina il secondo <xref:System.Windows.Forms.Button> controllo `cancelAsyncButton`e impostare il <xref:System.Windows.Forms.Control.Text%2A> proprietà `Cancel Async`. Impostare il relativo <xref:System.Windows.Forms.Control.Enabled%2A> proprietà `false`.  
  
6.  Creare un gestore eventi per entrambi i <xref:System.Windows.Forms.Button> dei controlli <xref:System.Windows.Forms.Control.Click> eventi. Per informazioni dettagliate, vedere [Procedura: Creare le impostazioni delle applicazioni usando la finestra di progettazione](http://msdn.microsoft.com/library/8461e9b8-14e8-406f-936e-3726732b23d2).  
  
7.  Trascinare un <xref:System.Windows.Forms.Label> controllo il **della casella degli strumenti** nel form e rinominarlo `resultLabel`.  
  
8.  Trascinare un <xref:System.Windows.Forms.ProgressBar> controllo il **della casella degli strumenti** nel form.  
  
## <a name="creating-a-backgroundworker-in-your-form"></a>Creazione di un BackgroundWorker nel modulo  
 È possibile creare il <xref:System.ComponentModel.BackgroundWorker> per l'operazione asincrona utilizzando il **Windows** **progettazione form**.  
  
#### <a name="to-create-a-backgroundworker-with-the-designer"></a>Per creare un BackgroundWorker con la finestra di progettazione  
  
-   Dal **componenti** scheda della finestra di **della casella degli strumenti**, trascinare un <xref:System.ComponentModel.BackgroundWorker> nel form.  
  
## <a name="adding-asynchronous-event-handlers"></a>Aggiunta dei gestori eventi asincroni  
 A questo punto si è pronti aggiungere gestori eventi per il <xref:System.ComponentModel.BackgroundWorker> eventi asincroni del componente. L'operazione dispendiosa in termini di tempo che verrà eseguita in background, ossia quella che calcola i numeri Fibonacci, viene chiamata da uno di questi gestori eventi.  
  
#### <a name="to-implement-asynchronous-event-handlers"></a>Per implementare i gestori eventi asincroni  
  
1.  Nel **proprietà** finestra, con la <xref:System.ComponentModel.BackgroundWorker> componente ancora selezionato, fare clic su di **eventi** pulsante. Fare doppio clic su di <xref:System.ComponentModel.BackgroundWorker.DoWork> e <xref:System.ComponentModel.BackgroundWorker.RunWorkerCompleted> gli eventi per creare gestori eventi. Per altre informazioni sulle modalità di utilizzo dei gestori eventi, vedere [Procedura: creare le impostazioni delle applicazioni usando la finestra di progettazione](http://msdn.microsoft.com/library/8461e9b8-14e8-406f-936e-3726732b23d2).  
  
2.  Creare nel form un nuovo metodo denominato `ComputeFibonacci`. L'operazione verrà effettivamente svolta da questo metodo che verrà eseguito in background. Il codice dimostra l'implementazione ricorsiva dell'algoritmo Fibonacci che è decisamente inefficiente e esponenzialmente impiega più tempo per completare i numeri a molte cifre. Viene impiegato per dimostrare come un'operazione possa provocare lunghi ritardi nell'applicazione.  
  
     [!code-cpp[System.ComponentModel.BackgroundWorker#10](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/CPP/fibonacciform.cpp#10)]
     [!code-csharp[System.ComponentModel.BackgroundWorker#10](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/CS/fibonacciform.cs#10)]
     [!code-vb[System.ComponentModel.BackgroundWorker#10](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/VB/fibonacciform.vb#10)]  
  
3.  Nel <xref:System.ComponentModel.BackgroundWorker.DoWork> gestore, aggiungere una chiamata al `ComputeFibonacci` metodo. Eseguire il primo parametro per `ComputeFibonacci` dal <xref:System.ComponentModel.DoWorkEventArgs.Argument%2A> proprietà del <xref:System.ComponentModel.DoWorkEventArgs>. Il <xref:System.ComponentModel.BackgroundWorker> e <xref:System.ComponentModel.DoWorkEventArgs> parametri verranno usati successivamente per i report di stato di avanzamento e annullamento supportano. Assegnare il valore restituito da `ComputeFibonacci` per il <xref:System.ComponentModel.DoWorkEventArgs.Result%2A> proprietà del <xref:System.ComponentModel.DoWorkEventArgs>. Il risultato sarà disponibile per il <xref:System.ComponentModel.BackgroundWorker.RunWorkerCompleted> gestore dell'evento.  
  
    > [!NOTE]
    >  Il <xref:System.ComponentModel.BackgroundWorker.DoWork> gestore dell'evento non fa riferimento il `backgroundWorker1` istanza variabile direttamente, per evitare di associare questo gestore eventi per un'istanza specifica di <xref:System.ComponentModel.BackgroundWorker>. Al contrario, un riferimento al <xref:System.ComponentModel.BackgroundWorker> che ha generato l'evento viene recuperato dal `sender` parametro. Questo è importante quando il form include più di un <xref:System.ComponentModel.BackgroundWorker>. È inoltre importante non modificare oggetti dell'interfaccia utente nel <xref:System.ComponentModel.BackgroundWorker.DoWork> gestore dell'evento. Comunicare invece con l'interfaccia utente tramite il <xref:System.ComponentModel.BackgroundWorker> eventi.  
  
     [!code-cpp[System.ComponentModel.BackgroundWorker#5](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/CPP/fibonacciform.cpp#5)]
     [!code-csharp[System.ComponentModel.BackgroundWorker#5](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/CS/fibonacciform.cs#5)]
     [!code-vb[System.ComponentModel.BackgroundWorker#5](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/VB/fibonacciform.vb#5)]  
  
4.  Nel `startAsyncButton` del controllo <xref:System.Windows.Forms.Control.Click> gestore, aggiungere il codice che avvia l'operazione asincrona.  
  
     [!code-cpp[System.ComponentModel.BackgroundWorker#13](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/CPP/fibonacciform.cpp#13)]
     [!code-csharp[System.ComponentModel.BackgroundWorker#13](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/CS/fibonacciform.cs#13)]
     [!code-vb[System.ComponentModel.BackgroundWorker#13](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/VB/fibonacciform.vb#13)]  
  
5.  Nel <xref:System.ComponentModel.BackgroundWorker.RunWorkerCompleted> gestore dell'evento, assegnare il risultato del calcolo per il `resultLabel` controllo.  
  
     [!code-cpp[System.ComponentModel.BackgroundWorker#6](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/CPP/fibonacciform.cpp#6)]
     [!code-csharp[System.ComponentModel.BackgroundWorker#6](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/CS/fibonacciform.cs#6)]
     [!code-vb[System.ComponentModel.BackgroundWorker#6](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/VB/fibonacciform.vb#6)]  
  
## <a name="adding-progress-reporting-and-support-for-cancellation"></a>Aggiunta dei report sullo stato di avanzamento e supporto per l'annullamento  
 Per le operazioni asincrone che impiegano molto tempo è spesso opportuno notificare all'utente lo stato di avanzamento e permettergli di annullare eventualmente l'operazione. La <xref:System.ComponentModel.BackgroundWorker> classe fornisce un evento che consente di inviare lo stato mentre l'operazione procede in background. Fornisce inoltre un flag che consente al codice rilevare una chiamata a <xref:System.ComponentModel.BackgroundWorker.CancelAsync%2A> e interrompersi.  
  
#### <a name="to-implement-progress-reporting"></a>Per implementare i report sullo stato di avanzamento  
  
1.  Nella finestra **Proprietà** selezionare `backgroundWorker1`. Impostare il <xref:System.ComponentModel.BackgroundWorker.WorkerReportsProgress%2A> e <xref:System.ComponentModel.BackgroundWorker.WorkerSupportsCancellation%2A> proprietà `true`.  
  
2.  Nel modulo `FibonacciCalculator` dichiarare due variabili che verranno utilizzate per tenere traccia dello stato di avanzamento.  
  
     [!code-cpp[System.ComponentModel.BackgroundWorker#14](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/CPP/fibonacciform.cpp#14)]
     [!code-csharp[System.ComponentModel.BackgroundWorker#14](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/CS/fibonacciform.cs#14)]
     [!code-vb[System.ComponentModel.BackgroundWorker#14](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/VB/fibonacciform.vb#14)]  
  
3.  Aggiunge un gestore eventi per l'evento <xref:System.ComponentModel.BackgroundWorker.ProgressChanged>. Nel <xref:System.ComponentModel.BackgroundWorker.ProgressChanged> gestore dell'evento, l'aggiornamento di <xref:System.Windows.Forms.ProgressBar> con il <xref:System.ComponentModel.ProgressChangedEventArgs.ProgressPercentage%2A> proprietà del <xref:System.ComponentModel.ProgressChangedEventArgs> parametro.  
  
     [!code-cpp[System.ComponentModel.BackgroundWorker#7](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/CPP/fibonacciform.cpp#7)]
     [!code-csharp[System.ComponentModel.BackgroundWorker#7](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/CS/fibonacciform.cs#7)]
     [!code-vb[System.ComponentModel.BackgroundWorker#7](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/VB/fibonacciform.vb#7)]  
  
#### <a name="to-implement-support-for-cancellation"></a>Per implementare il supporto per l'annullamento  
  
1.  Nel `cancelAsyncButton` del controllo <xref:System.Windows.Forms.Control.Click> gestore, aggiungere il codice che consente di annullare l'operazione asincrona.  
  
     [!code-cpp[System.ComponentModel.BackgroundWorker#4](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/CPP/fibonacciform.cpp#4)]
     [!code-csharp[System.ComponentModel.BackgroundWorker#4](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/CS/fibonacciform.cs#4)]
     [!code-vb[System.ComponentModel.BackgroundWorker#4](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/VB/fibonacciform.vb#4)]  
  
2.  I seguenti frammenti di codice nel metodo `ComputeFibonacci` restituiscono lo stato di avanzamento e supportano l'annullamento.  
  
     [!code-cpp[System.ComponentModel.BackgroundWorker#11](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/CPP/fibonacciform.cpp#11)]
     [!code-csharp[System.ComponentModel.BackgroundWorker#11](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/CS/fibonacciform.cs#11)]
     [!code-vb[System.ComponentModel.BackgroundWorker#11](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/VB/fibonacciform.vb#11)]  
    [!code-cpp[System.ComponentModel.BackgroundWorker#12](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/CPP/fibonacciform.cpp#12)]
    [!code-csharp[System.ComponentModel.BackgroundWorker#12](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/CS/fibonacciform.cs#12)]
    [!code-vb[System.ComponentModel.BackgroundWorker#12](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker/VB/fibonacciform.vb#12)]  
  
## <a name="checkpoint"></a>Checkpoint  
 A questo punto è possibile compilare ed eseguire l'applicazione Fibonacci Calculator.  
  
#### <a name="to-test-your-project"></a>Per eseguire il test del progetto  
  
-   Premere F5 per compilare ed eseguire l'applicazione.  
  
     Durante il calcolo è in esecuzione in background, verrà visualizzato il <xref:System.Windows.Forms.ProgressBar> visualizzando lo stato di avanzamento del calcolo in fase di completamento. È anche possibile annullare l'operazione in sospeso.  
  
     Per i numeri con poche cifre, il calcolo dovrebbe essere molto rapido, ma per i numeri con tante cifre, si potrebbe notare un considerevole ritardo. Se si immette il valore 30 o superiore, il ritardo sarà di diversi secondi, a seconda della velocità del computer. Per i valori maggiori di 40, potrebbero essere necessari diversi minuti o ore per completare il calcolo. Mentre il calcolatore è impegnato a calcolare un numero Fibonacci con tante cifre, il modulo può essere spostato liberamente, ridotto a icona, ingrandito e persino chiuso in quanto il thread principale dell'interfaccia utente non è in attesa della fine del calcolo.  
  
## <a name="next-steps"></a>Passaggi successivi  
 Ora che è stato implementato un form che usa un <xref:System.ComponentModel.BackgroundWorker> componente per eseguire un calcolo in background, è possibile esplorare altre possibilità per le operazioni asincrone:  
  
-   Utilizzare più <xref:System.ComponentModel.BackgroundWorker> oggetti per diverse operazioni simultanee.  
  
-   Per eseguire il debug dell'applicazione con multithreading, vedere [Procedura: utilizzare la finestra Thread](/visualstudio/debugger/how-to-use-the-threads-window).  
  
-   Implementare il componente che supporta il modello di programmazione asincrona. Per ulteriori informazioni, vedere [Cenni preliminari sul modello asincrono basato su eventi](../../../../docs/standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-overview.md).  
  
    > [!CAUTION]
    >  L'uso di qualsiasi tipo di multithreading determina la potenziale esposizione a bug seri e complessi. Vedere [Procedure consigliate per l'uso del threading gestito](../../../../docs/standard/threading/managed-threading-best-practices.md) prima di implementare soluzioni che usano il multithreading.  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.ComponentModel.BackgroundWorker>  
 [Suggerimenti per l'utilizzo del threading gestito](../../../../docs/standard/threading/managed-threading-best-practices.md)  
 [Multithreading nei componenti](http://msdn.microsoft.com/library/2fc31e68-fb71-4544-b654-0ce720478779)  
 [NOT IN BUILD: Multithreading in Visual Basic](http://msdn.microsoft.com/library/c731a50c-09c1-4468-9646-54c86b75d269)  
 [Procedura: Implementare un form che esegue un'operazione in background](../../../../docs/framework/winforms/controls/how-to-implement-a-form-that-uses-a-background-operation.md)  
 [Procedura dettagliata: Esecuzione di un'operazione in background](../../../../docs/framework/winforms/controls/walkthrough-running-an-operation-in-the-background.md)  
 [BackgroundWorker (componente)](../../../../docs/framework/winforms/controls/backgroundworker-component.md)
