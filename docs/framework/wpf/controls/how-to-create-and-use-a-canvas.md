---
title: 'Procedura: creare e utilizzare un''area di disegno'
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-wpf
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- csharp
- vb
helpviewer_keywords:
- controls [WPF], Canvas
- Canvas control [WPF], creating
- Canvas control [WPF], using
ms.assetid: 420b9487-9a15-477c-9489-a22a4dec7779
caps.latest.revision: "12"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 562531f75d6a800ff93a02709a053b790de52ea2
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/22/2017
---
# <a name="how-to-create-and-use-a-canvas"></a>Procedura: creare e utilizzare un'area di disegno
In questo esempio viene illustrato come creare e utilizzare un'istanza di <xref:System.Windows.Controls.Canvas>.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene posizionato in modo esplicito due <xref:System.Windows.Controls.TextBlock> elementi utilizzando il <xref:System.Windows.Controls.Canvas.SetTop%2A> e <xref:System.Windows.Controls.Canvas.SetLeft%2A> metodi di <xref:System.Windows.Controls.Canvas>. Nell'esempio viene inoltre assegnato un <xref:System.Windows.Controls.Control.Background%2A> colore di `LightSteelBlue` per il <xref:System.Windows.Controls.Canvas>.  
  
> [!NOTE]
>  Quando si utilizza [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] posizione <xref:System.Windows.Controls.TextBlock> elementi, utilizzare il <xref:System.Windows.Controls.Canvas.Top%2A> e <xref:System.Windows.Controls.Canvas.Left%2A> proprietà.  
  
 [!code-csharp[CanvasCode#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CanvasCode/CSharp/Canvas_Code.cs#1)]
 [!code-vb[CanvasCode#1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/CanvasCode/VisualBasic/canvas_vb.vb#1)]  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Windows.Controls.Canvas>  
 <xref:System.Windows.Controls.TextBlock>  
 <xref:System.Windows.Controls.Canvas.SetTop%2A>  
 <xref:System.Windows.Controls.Canvas.SetLeft%2A>  
 <xref:System.Windows.Controls.Canvas.Top%2A>  
 <xref:System.Windows.Controls.Canvas.Left%2A>  
 [Cenni preliminari sugli elementi Panel](../../../../docs/framework/wpf/controls/panels-overview.md)  
 [Procedure relative alle proprietà](../../../../docs/framework/wpf/controls/canvas-how-to-topics.md)
