---
title: Tipo XAML intrinseco x:XData
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-wpf
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- x:XData
- XData
- xXData
helpviewer_keywords:
- XAML [XAML Services], x:XData directive element
- XData in XAML [XAML Services]
- x:XData XAML directive element [XAML Services]
ms.assetid: 7ce209c2-621b-4977-b643-565f7e663534
caps.latest.revision: "17"
author: wadepickett
ms.author: wpickett
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: ec46d0363e5b10d3bd3bd3f9c8f4d3694abc1c8d
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/22/2017
---
# <a name="xxdata-intrinsic-xaml-type"></a>Tipo XAML intrinseco x:XData
Consente il posizionamento di isole di dati XML all'interno di una produzione XAML. Elementi XML all'interno di `x:XData` non devono essere considerati dai processori XAML come se facessero parte dello spazio dei nomi XAML predefinito attivo o qualsiasi altro spazio dei nomi XAML. `x:XData`può contenere XML ben formato arbitrario.  
  
## <a name="xaml-object-element-usage"></a>Utilizzo della sintassi XAML per gli elementi oggetto  
  
```  
<x:XData>  
  <elementDataRoot>  
    [elementData]  
  </elementDataRoot>  
</x:XData>  
```  
  
## <a name="xaml-values"></a>Valori XAML  
  
|||  
|-|-|  
|`elementDataRoot`|Il singolo elemento radice dell'isola di dati. Per la maggior parte dei consumer finali, XML che non dispone di un solo nodo radice è considerato non valido. In particolare, è necessario un solo nodo radice se il `x:XData` un'origine dati XML è destinato ad WPF o molte altre tecnologie che utilizzano origini XML per l'associazione dati.|  
|`[elementData]`|Facoltativo. File XML che rappresenta i dati XML. Qualsiasi numero di elementi può essere contenuto i dati dell'elemento e gli elementi nidificati possono essere contenuti in altri elementi. Tuttavia, si applicano le regole generali di XML.|  
  
## <a name="remarks"></a>Note  
 Gli elementi XML all'interno di un `x:XData` oggetto può dichiarare nuovamente tutti i possibili spazi dei nomi e i prefissi del XMLDOM all'interno dei dati.  
  
 Accesso a livello di codice ai dati XML e `x:XData` tipo XAML intrinseco è possibile nei servizi XAML di .NET Framework tramite la <xref:System.Windows.Markup.XData> classe.  
  
## <a name="wpf-usage-notes"></a>Note sull'utilizzo WPF  
 Il `x:XData` oggetto viene utilizzato principalmente come un oggetto figlio di un <xref:System.Windows.Data.XmlDataProvider>, o in alternativa, come oggetto figlio di <xref:System.Windows.Data.XmlDataProvider.XmlSerializer%2A?displayProperty=nameWithType> proprietà (in XAML, viene espressa nella sintassi degli elementi di proprietà).  
  
 I dati in genere devono ridefinire lo spazio dei nomi XML di base all'interno dell'isola di dati da un nuovo spazio dei nomi XML predefinito (impostato su una stringa vuota). Si tratta di una più semplice per le isole di dati semplici in quanto il <xref:System.Windows.Data.Binding.XPath%2A> espressioni che consentono di fare riferimento e associare i dati possono evitare di includere i prefissi. Isole di dati più complesse potrebbero definire più prefissi per i dati e utilizzare un prefisso specifico per lo spazio dei nomi XML nella directory principale. In questo caso, tutti <xref:System.Windows.Data.Binding.XPath%2A> riferimenti a espressioni deve includere il prefisso di mapping dello spazio dei nomi appropriato. Per altre informazioni, vedere la [panoramica del data binding](../../../docs/framework/wpf/data/data-binding-overview.md).  
  
 Tecnicamente, `x:XData` può essere utilizzato come il contenuto di qualsiasi proprietà di tipo <xref:System.Xml.Serialization.IXmlSerializable>. Tuttavia, <xref:System.Windows.Data.XmlDataProvider.XmlSerializer%2A?displayProperty=nameWithType> è l'unica implementazione rilevante.  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Windows.Data.XmlDataProvider>  
 [Panoramica sul data binding](../../../docs/framework/wpf/data/data-binding-overview.md)  
 [Estensione di markup Binding](../../../docs/framework/wpf/advanced/binding-markup-extension.md)
