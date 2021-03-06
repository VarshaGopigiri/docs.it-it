---
title: 'Procedura dettagliata: creazione di una pipeline del flusso di dati'
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-standard
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- csharp
- vb
helpviewer_keywords:
- dataflow pipelines, creating with TPL
- Task Parallel Library, dataflows
- TPL dataflow library, creating dataflow pipeline
ms.assetid: 69308f82-aa22-4ac5-833d-e748533b58e8
caps.latest.revision: "11"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: d63fb872382bfc0a3ba3b8637c7357ab65c58fbf
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/18/2017
---
# <a name="walkthrough-creating-a-dataflow-pipeline"></a>Procedura dettagliata: creazione di una pipeline del flusso di dati
Sebbene sia possibile utilizzare il <xref:System.Threading.Tasks.Dataflow.DataflowBlock.Receive%2A?displayProperty=nameWithType>, <xref:System.Threading.Tasks.Dataflow.DataflowBlock.ReceiveAsync%2A?displayProperty=nameWithType>, e <xref:System.Threading.Tasks.Dataflow.DataflowBlock.TryReceive%2A?displayProperty=nameWithType> metodi per ricevere messaggi da blocchi di origine, è anche possibile connettere blocchi dei messaggi per creare un *della pipeline del flusso di dati*. Una pipeline del flusso di dati è una serie di componenti, o *blocchi di flussi di dati*, ognuno dei quali esegue un'attività specifica che contribuisce a un obiettivo più grande. In ogni blocco di flussi di dati di una pipeline del flusso di dati viene eseguito un lavoro quando si riceve un messaggio da un altro blocco di flussi di dati. Un'analogia a questo è data da una catena di montaggio per la produzione di automobili. Man mano che ciascun veicolo passa attraverso la catena di montaggio, in una postazione viene assemblato il telaio, nella successiva viene installato il motore e così via. Grazie alla catena di montaggio in cui è possibile eseguire il montaggio di più veicoli contemporaneamente, si ottiene una maggiore produzione rispetto al montaggio completo dei veicoli uno alla volta.  
  
> [!TIP]
>  La libreria del flusso di dati TPL (spazio dei nomi <xref:System.Threading.Tasks.Dataflow?displayProperty=nameWithType>) non viene distribuita con [!INCLUDE[net_v45](../../../includes/net-v45-md.md)]. Per installare il <xref:System.Threading.Tasks.Dataflow> dello spazio dei nomi, Apri il progetto in [!INCLUDE[vs_dev11_long](../../../includes/vs-dev11-long-md.md)], scegliere **Gestisci pacchetti NuGet** dal menu progetto e cercare online il `Microsoft.Tpl.Dataflow` pacchetto.  
  
 Questo documento illustra una pipeline di flussi di dati che scarica il libro *l'Iliade di omero* da un sito Web e le ricerche di testo per la corrispondenza di singole parole con le stesse caratteri prima della parola. La formazione della pipeline del flusso di dati in questo documento consiste nei passaggi seguenti:  
  
1.  Creare i blocchi di flussi di dati che fanno parte della pipeline.  
  
2.  Connettere ogni blocco di flussi di dati al blocco successivo nella pipeline. L'output del blocco precedente nella pipeline viene ricevuto da ogni blocco come input.  
  
3.  Per ogni blocco di flussi di dati, creare un'attività di continuazione mediante la quale il blocco successivo viene impostato sullo stato completato al termine del blocco precedente.  
  
4.  Inserire i dati nell'intestazione della pipeline.  
  
5.  Contrassegnare l'intestazione della pipeline come completata.  
  
6.  Attendere il completamento di tutto il lavoro da parte della pipeline.  
  
## <a name="prerequisites"></a>Prerequisiti  
 Prima di iniziare questa procedura dettagliata, leggere [Flusso di dati](../../../docs/standard/parallel-programming/dataflow-task-parallel-library.md).  
  
## <a name="creating-a-console-application"></a>Creazione di un'applicazione console  
 In [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] creare un progetto di [!INCLUDE[csprcs](../../../includes/csprcs-md.md)] o di applicazione console di [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]. Aggiungere un riferimento a System.Threading.Tasks.Dataflow.dll.  
  
 In alternativa, creare un file e denominarlo `ReverseWords.cs` (`ReverseWords.vb` per [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]), quindi eseguire il comando seguente in una finestra del prompt dei comandi di Visual Studio per compilare il progetto.  
  
 [!INCLUDE[csprcs](../../../includes/csprcs-md.md)]  
  
 **csc.exe /r:System.Threading.Tasks.Dataflow.dll reversewords. cs**  
  
 [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]  
  
 **vbc.exe /r:System.Threading.Tasks.Dataflow.dll reversewords. vb**  
  
 Aggiungere il seguente codice al progetto per creare l'applicazione di base.  
  
 [!code-csharp[TPLDataflow_Palindromes#2](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_palindromes/cs/dataflowpalindromes.cs#2)]
 [!code-vb[TPLDataflow_Palindromes#2](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_palindromes/vb/dataflowpalindromes.vb#2)]  
  
## <a name="creating-the-dataflow-blocks"></a>Creazione dei blocchi di flussi di dati  
 Aggiungere il seguente codice al metodo `Main` per creare i blocchi di flussi di dati che fanno parte della pipeline. Nella tabella seguente viene riepilogato il ruolo di ciascun membro della pipeline.  
  
 [!code-csharp[TPLDataflow_Palindromes#3](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_palindromes/cs/dataflowpalindromes.cs#3)]
 [!code-vb[TPLDataflow_Palindromes#3](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_palindromes/vb/dataflowpalindromes.vb#3)]  
  
|Membro|Tipo|Descrizione|  
|------------|----------|-----------------|  
|`downloadString`|<xref:System.Threading.Tasks.Dataflow.TransformBlock%602>|Scarica il testo del libro dal Web.|  
|`createWordList`|<xref:System.Threading.Tasks.Dataflow.TransformBlock%602>|Suddivide il testo del libro in una matrice di parole.|  
|`filterWordList`|<xref:System.Threading.Tasks.Dataflow.TransformBlock%602>|Rimuove le parole brevi dalla matrice di parole, ordina le parole risultanti in ordine alfabetico e rimuove i duplicati.|  
|`findReversedWords`|<xref:System.Threading.Tasks.Dataflow.TransformManyBlock%602>|Cerca tutte le parole nella raccolta filtrata della matrice di parole i cui contrari sono presenti anche nella matrice di parole.|  
|`printReversedWords`|<xref:System.Threading.Tasks.Dataflow.ActionBlock%601>|Visualizza le parole e i contrari corrispondenti nella console.|  
  
 Sebbene sia possibile combinare più passaggi nella pipeline del flusso di dati in questo esempio in un unico passaggio, nell'esempio viene illustrato il concetto di composizione di più attività del flusso di dati indipendenti per eseguire un'attività più grande. Nell'esempio viene usato l'oggetto <xref:System.Threading.Tasks.Dataflow.TransformBlock%602> per consentire a ogni membro della pipeline di eseguire un'operazione sui relativi dati di input e inviare i risultati al passaggio successivo nella pipeline. Il membro `findReversedWords` della pipeline è un oggetto <xref:System.Threading.Tasks.Dataflow.TransformManyBlock%602> poiché tramite esso vengono generati più output indipendenti per ogni input. La parte finale della pipeline, `printReversedWords`, è un oggetto <xref:System.Threading.Tasks.Dataflow.ActionBlock%601> poiché tramite esso viene eseguita un'azione sul relativo input e non viene generato un risultato.  
  
## <a name="forming-the-pipeline"></a>Formazione della pipeline  
 Aggiungere il codice seguente per connettere ogni blocco al successivo nella pipeline.  
  
 Quando si chiama il metodo <xref:System.Threading.Tasks.Dataflow.DataflowBlock.LinkTo%2A> per connettere un blocco di origine del flusso di dati a un blocco di destinazione del flusso di dati, i dati nel blocco di origine del flusso di dati vengono propagati nel blocco di destinazione quando diventano disponibili.  
  
 [!code-csharp[TPLDataflow_Palindromes#4](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_palindromes/cs/dataflowpalindromes.cs#4)]
 [!code-vb[TPLDataflow_Palindromes#4](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_palindromes/vb/dataflowpalindromes.vb#4)]  
  
## <a name="creating-the-completion-tasks"></a>Creazione delle attività di completamento  
 Aggiungere il codice seguente per consentire a ogni blocco del flusso di dati di eseguire un'azione finale dopo l'elaborazione di tutti i dati.  
  
 [!code-csharp[TPLDataflow_Palindromes#5](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_palindromes/cs/dataflowpalindromes.cs#5)]
 [!code-vb[TPLDataflow_Palindromes#5](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_palindromes/vb/dataflowpalindromes.vb#5)]  
  
 Per propagare il completamento attraverso la pipeline, mediante ogni attività di completamento il blocco di flussi di dati successivo viene impostato sullo stato completato. Ad esempio, quando l'intestazione della pipeline è impostata sullo stato completato, vengono elaborati tutti i messaggi rimanenti memorizzati nel buffer e viene quindi eseguita la relativa attività di completamento, mediante la quale viene impostato il secondo membro della pipeline sullo stato completato. Tramite il secondo membro della pipeline, a sua volta, vengono elaborati tutti i messaggi rimanenti memorizzati nel buffer e viene quindi eseguita la relativa attività di completamento, mediante la quale viene impostato il terzo membro della pipeline sullo stato completato. Questo processo continua fino al completamento di tutti i membri della pipeline. In questo esempio viene usata la parola chiave `delegate` (`Function` in [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]) per definire le attività di continuazione.  
  
## <a name="posting-data-to-the-pipeline"></a>Inserimento dei dati nella pipeline  
 Aggiungere il codice seguente per registrare l'URL del libro *l'Iliade di omero* all'intestazione della pipeline del flusso di dati.  
  
 [!code-csharp[TPLDataflow_Palindromes#6](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_palindromes/cs/dataflowpalindromes.cs#6)]
 [!code-vb[TPLDataflow_Palindromes#6](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_palindromes/vb/dataflowpalindromes.vb#6)]  
  
 In questo esempio viene usato il metodo <xref:System.Threading.Tasks.Dataflow.DataflowBlock.Post%2A?displayProperty=nameWithType> in modo sincrono per inviare i dati all'intestazione della pipeline. Usare il metodo <xref:System.Threading.Tasks.Dataflow.DataflowBlock.SendAsync%2A?displayProperty=nameWithType> quando è necessario inviare in modo asincrono i dati a un nodo del flusso di dati.  
  
## <a name="completing-pipeline-activity"></a>Completamento dell'attività della pipeline  
 Aggiungere il codice seguente per contrassegnare l'intestazione della pipeline come completata. Nell'intestazione della pipeline viene eseguita la relativa attività di continuazione al termine dell'elaborazione di tutti i messaggi memorizzati nel buffer. Tramite questa attività di continuazione lo stato completato viene propagato attraverso la pipeline.  
  
 [!code-csharp[TPLDataflow_Palindromes#7](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_palindromes/cs/dataflowpalindromes.cs#7)]
 [!code-vb[TPLDataflow_Palindromes#7](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_palindromes/vb/dataflowpalindromes.vb#7)]  
  
 In questo esempio viene inviato un URL tramite la pipeline del flusso di dati da elaborare. Se si invia più di un input attraverso una pipeline, chiamare il metodo <xref:System.Threading.Tasks.Dataflow.IDataflowBlock.Complete%2A?displayProperty=nameWithType> dopo l'invio di tutti gli input. È possibile omettere questo passaggio se nell'applicazione non vi è alcun punto ben definito in cui i dati non sono più disponibili o non è necessaria l'attesa del completamento della pipeline da parte dell'applicazione.  
  
## <a name="waiting-for-the-pipeline-to-finish"></a>Attesa del completamento della pipeline  
 Aggiungere il codice seguente per attendere il completamento della pipeline. Poiché in questo esempio vengono usate le attività di continuazione per propagare il completamento attraverso la pipeline, l'operazione globale viene completata al termine della parte finale della pipeline.  
  
 [!code-csharp[TPLDataflow_Palindromes#8](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_palindromes/cs/dataflowpalindromes.cs#8)]
 [!code-vb[TPLDataflow_Palindromes#8](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_palindromes/vb/dataflowpalindromes.vb#8)]  
  
 È possibile attendere il completamento del flusso di dati da qualsiasi thread o da più thread contemporaneamente.  
  
## <a name="the-complete-example"></a>Esempio completo  
 Nell'esempio riportato di seguito viene illustrato il codice completo per questa procedura guidata.  
  
 [!code-csharp[TPLDataflow_Palindromes#1](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_palindromes/cs/dataflowpalindromes.cs#1)]
 [!code-vb[TPLDataflow_Palindromes#1](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_palindromes/vb/dataflowpalindromes.vb#1)]  
  
## <a name="next-steps"></a>Passaggi successivi  
 In questo esempio viene inviato un URL da elaborare tramite la pipeline del flusso di dati. Se si invia più di un valore di input tramite una pipeline, è possibile introdurre un form di parallelismo nell'applicazione che rappresenta il numero di parti che possono essere spostate in una fabbrica di automobili. Quando tramite il primo membro della pipeline viene inviato il risultato al secondo membro, è possibile elaborare un altro elemento in parallelo mentre tramite il secondo membro viene elaborato il primo risultato.  
  
 Il parallelismo raggiunto attraverso l'utilizzo di pipeline del flusso di dati è noto come *parallelismo con granularità grossolana* perché è in genere è costituito da un numero inferiore di attività più grandi. È inoltre possibile utilizzare più *parallelismo con granularità fine* di attività più piccole a esecuzione breve in una pipeline del flusso di dati. In questo esempio nel membro `findReversedWords` della pipeline viene usato il metodo <xref:System.Threading.Tasks.Parallel.ForEach%2A?displayProperty=nameWithType> per elaborare in parallelo più elementi nell'elenco di lavoro. L'utilizzo di parallelismo con granularità fine in una pipeline con granularità grossolana può migliorare la velocità effettiva globale.  
  
 È inoltre possibile connettere un blocco di flussi di dati di origine a più blocchi di destinazione per creare un *rete del flusso di dati*. La versione sottoposta a overload del metodo <xref:System.Threading.Tasks.Dataflow.DataflowBlock.LinkTo%2A> accetta un oggetto <xref:System.Predicate%601> mediante il quale viene definito se il blocco di destinazione accetta ogni messaggio in base al relativo valore. La maggior parte dei tipi di blocchi di flussi di dati usati come origini offrono messaggi a tutti i blocchi di destinazione connessi, nell'ordine in cui sono stati collegati, finché uno dei blocchi non accetta il messaggio. Tramite questo meccanismo di filtro, è possibile creare sistemi di blocchi di flussi di dati connessi in cui determinati dati vengono indirizzati tramite un percorso mentre altri tramite un altro percorso. Per un esempio che usa il filtro per creare una rete del flusso di dati, vedere [procedura dettagliata: flussi di dati in un'applicazione Windows Form utilizzando](../../../docs/standard/parallel-programming/walkthrough-using-dataflow-in-a-windows-forms-application.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Flusso di dati](../../../docs/standard/parallel-programming/dataflow-task-parallel-library.md)
