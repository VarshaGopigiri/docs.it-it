---
title: "Proprietà di dipendenza di sola lettura"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-wpf
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- dependency properties [WPF], read-only
- read-only dependency properties [WPF]
ms.assetid: f23d6ec9-3780-4c09-a2ff-b2f0a2deddf1
caps.latest.revision: "8"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 31e4080416d5eb4fdfe5c33ec2b65e1dced6d012
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/22/2017
---
# <a name="read-only-dependency-properties"></a>Proprietà di dipendenza di sola lettura
Questo argomento descrive le proprietà di dipendenza di sola lettura, incluse le proprietà di dipendenza di sola lettura esistenti e gli scenari e le tecniche per la creazione di una proprietà di dipendenza di sola lettura personalizzata.  
  

  
<a name="prerequisites"></a>   
## <a name="prerequisites"></a>Prerequisiti  
 Nell'argomento si presuppone la conoscenza degli scenari di base dell'implementazione di una proprietà di dipendenza e del modo in cui i metadati vengono applicati a una proprietà di dipendenza personalizzata. Per il contesto, vedere [Proprietà di dipendenza personalizzate](../../../../docs/framework/wpf/advanced/custom-dependency-properties.md) e [Metadati delle proprietà di dipendenza](../../../../docs/framework/wpf/advanced/dependency-property-metadata.md).  
  
<a name="existing"></a>   
## <a name="existing-read-only-dependency-properties"></a>Proprietà di dipendenza di sola lettura esistenti  
 Alcune delle proprietà di dipendenza definite nel framework [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] sono di sola lettura. La ragione più comune per specificare una proprietà di dipendenza di sola lettura è che si tratta di proprietà che devono essere usate per la determinazione dello stato. Se però lo stato è influenzato da una molteplicità di fattori, la semplice impostazione della proprietà su quello stato non rappresenta la soluzione appropriata nell'ottica della progettazione di un'interfaccia utente. Ad esempio, la proprietà <xref:System.Windows.UIElement.IsMouseOver%2A> è semplicemente lo stato superficiale determinato dall'input del mouse. Ogni tentativo di impostare questo valore a livello di codice aggirando il vero input del mouse sarebbe imprevedibile e potrebbe causare incongruenze.  
  
 Dal momento che non possono essere impostate, le proprietà di dipendenza di sola lettura non sono appropriate per molti degli scenari in cui in genere offrono una soluzione (vale a dire: data binding, possibilità di applicare direttamente uno stile a un valore, convalida, animazione, ereditarietà). Nonostante non possano essere impostate, queste proprietà hanno in ogni caso alcune delle funzionalità aggiuntive supportate dalle proprietà di dipendenza nel sistema di proprietà. La funzionalità più importante consiste nel fatto che la proprietà di dipendenza di sola lettura può essere usata come trigger di proprietà in uno stile. Non è possibile abilitare trigger con una proprietà [!INCLUDE[TLA#tla_clr](../../../../includes/tlasharptla-clr-md.md)] standard, è necessaria una proprietà di dipendenza. Argomento <xref:System.Windows.UIElement.IsMouseOver%2A> proprietà è un esempio perfetto di uno scenario in cui potrebbe essere utile definire lo stile per un controllo, in cui alcune proprietà visible, ad esempio uno sfondo, in primo piano o proprietà simili di elementi composti all'interno di controllo cambia quando l'utente posiziona il mouse su un'area definita del controllo. Le modifiche a una proprietà di dipendenza di sola lettura possono anche essere rilevate e segnalate dai processi di invalidamento inerenti del sistema di proprietà, che infatti è dotato del supporto interno della funzionalità del trigger di proprietà.  
  
<a name="new"></a>   
## <a name="creating-custom-read-only-dependency-properties"></a>Creazione di proprietà di dipendenza di sola lettura personalizzate  
 Assicurarsi di leggere la sezione precedente sui motivi per cui le proprietà di dipendenza di sola lettura non funzionano per molti scenari comuni di proprietà di dipendenza. Se tuttavia si ha uno scenario adatto, è possibile creare una proprietà di dipendenza di sola lettura personalizzata.  
  
 Gran parte del processo di creazione di una proprietà di dipendenza di sola lettura è identico a quello descritto negli argomenti [Proprietà di dipendenza personalizzate](../../../../docs/framework/wpf/advanced/custom-dependency-properties.md) e [Implementare una proprietà di dipendenza](../../../../docs/framework/wpf/advanced/how-to-implement-a-dependency-property.md). Vi sono tre differenze importanti:  
  
-   Quando si registra la proprietà, chiamare il <xref:System.Windows.DependencyProperty.RegisterReadOnly%2A> metodo anziché la normale <xref:System.Windows.DependencyProperty.Register%2A> metodo per la registrazione della proprietà.  
  
-   Quando si implementa la proprietà del "wrapper" [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)], verificare che nemmeno il wrapper abbia un'implementazione impostata, in modo che non esista alcuna incongruenza nello stato di sola lettura per il wrapper pubblico che si espone.  
  
-   L'oggetto restituito dalla registrazione di sola lettura è <xref:System.Windows.DependencyPropertyKey> anziché <xref:System.Windows.DependencyProperty>. Anche se è necessario archiviare il campo come membro, questo in genere non viene reso un membro pubblico del tipo.  
  
 Naturalmente, il valore o campo privato sottostante della proprietà di dipendenza di sola lettura può essere scritto usando qualsiasi logica. Il modo più semplice per impostare la proprietà inizialmente o come parte della logica di runtime consiste nell'usare le [!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)] del sistema di proprietà anziché aggirare il sistema di proprietà e impostare direttamente il campo sottostante privato. In particolare, è disponibile una firma di <xref:System.Windows.DependencyObject.SetValue%2A> che accetta un parametro di tipo <xref:System.Windows.DependencyPropertyKey>. Come e dove questo valore è impostato a livello di codice all'interno della logica dell'applicazione influirà come si desidera impostare l'accesso per il <xref:System.Windows.DependencyPropertyKey> creato durante la registrazione prima di tutto la proprietà di dipendenza. Se si gestisce tutta questa logica all'interno della classe è possibile renderla privata o, se è necessario impostarla da un'altra porzione dell'assembly, è possibile impostarla come interna. Un approccio consiste nel chiamare <xref:System.Windows.DependencyObject.SetValue%2A> all'interno di un gestore eventi di classe di un evento rilevante che informa l'istanza di una classe che è necessario modificare il valore della proprietà archiviato. Un altro approccio consiste nel collegare le proprietà di dipendenza utilizzando <xref:System.Windows.PropertyChangedCallback> e <xref:System.Windows.CoerceValueCallback> callback come parte dei metadati di quelle proprietà durante la registrazione.  
  
 Poiché il <xref:System.Windows.DependencyPropertyKey> è privato e non viene propagata dal sistema di proprietà di fuori del codice, una proprietà di dipendenza di sola lettura delle impostazioni migliore sicurezza rispetto a una proprietà di dipendenza di sola lettura. Per una proprietà di dipendenza di lettura e scrittura, il campo di identificazione è pubblico in modo esplicito oppure implicito, per cui la proprietà può essere impostata senza alcuna limitazione. Per informazioni più specifiche, vedere [Sicurezza della proprietà di dipendenza](../../../../docs/framework/wpf/advanced/dependency-property-security.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Panoramica sulle proprietà di dipendenza](../../../../docs/framework/wpf/advanced/dependency-properties-overview.md)  
 [Proprietà di dipendenza personalizzate](../../../../docs/framework/wpf/advanced/custom-dependency-properties.md)  
 [Applicazione di stili e modelli](../../../../docs/framework/wpf/controls/styling-and-templating.md)
