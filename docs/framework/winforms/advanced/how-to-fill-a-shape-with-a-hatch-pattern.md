---
title: 'Procedura: riempire una forma con un motivo a tratteggio'
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
helpviewer_keywords:
- patterns [Windows Forms], adding to shapes
- shapes [Windows Forms], filling with patterns
- brushes [Windows Forms], using hatch brushes
ms.assetid: 9c8300ff-187b-404f-af1f-ebd499f5b16f
caps.latest.revision: "16"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: f44289b79812f2330639cc333727bd21b6ef4fe6
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/22/2017
---
# <a name="how-to-fill-a-shape-with-a-hatch-pattern"></a>Procedura: riempire una forma con un motivo a tratteggio
Un motivo a tratteggio è composto da due colori: uno per lo sfondo e uno per le righe che formano il modello sullo sfondo. Per riempire una forma chiusa con un motivo a tratteggio, utilizzare un <xref:System.Drawing.Drawing2D.HatchBrush> oggetto. Nell'esempio riportato di seguito viene illustrato come compilare un'ellisse con un motivo a tratteggio:  
  
## <a name="example"></a>Esempio  
 Il <xref:System.Drawing.Drawing2D.HatchBrush.%23ctor%2A> costruttore accetta tre argomenti: il colore di sfondo, il colore della linea di tratteggio e lo stile di tratteggio. L'argomento dello stile di tratteggio può essere un valore compreso tra il <xref:System.Drawing.Drawing2D.HatchStyle> enumerazione. Sono presenti più di 50 elementi di <xref:System.Drawing.Drawing2D.HatchStyle> enumerazione; alcuni di questi elementi sono visualizzati nell'elenco seguente:  
  
-   <xref:System.Drawing.Drawing2D.HatchStyle.Horizontal>  
  
-   <xref:System.Drawing.Drawing2D.HatchStyle.Vertical>  
  
-   <xref:System.Drawing.Drawing2D.HatchStyle.ForwardDiagonal>  
  
-   <xref:System.Drawing.Drawing2D.HatchStyle.BackwardDiagonal>  
  
-   <xref:System.Drawing.Drawing2D.HatchStyle.Cross>  
  
-   <xref:System.Drawing.Drawing2D.HatchStyle.DiagonalCross>  
  
 Nella figura seguente mostra l'ellisse piena.  
  
 ![Motivo di tratteggio](../../../../docs/framework/winforms/advanced/media/hatch1.png "hatch1")  
  
 [!code-csharp[System.Drawing.UsingABrush#41](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.UsingABrush/CS/Class1.cs#41)]
 [!code-vb[System.Drawing.UsingABrush#41](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.UsingABrush/VB/Class1.vb#41)]  
  
## <a name="compiling-the-code"></a>Compilazione del codice  
 L'esempio precedente è progettato per l'uso con Windows Form e richiede <xref:System.Windows.Forms.PaintEventArgs> `e`, ovvero un parametro del <xref:System.Windows.Forms.Control.Paint> gestore dell'evento.  
  
## <a name="see-also"></a>Vedere anche  
 [Uso di un oggetto Brush per il riempimento di forme](../../../../docs/framework/winforms/advanced/using-a-brush-to-fill-shapes.md)
