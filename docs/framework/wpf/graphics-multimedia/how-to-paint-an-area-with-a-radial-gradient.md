---
title: 'Procedura: disegnare un''area con una sfumatura radiale'
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
- brushes [WPF], painting with radial gradients
- radial gradients [WPF], painting with
- painting [WPF], with radial gradients
ms.assetid: b5d0fc8a-8986-4796-b003-a75b41a48928
caps.latest.revision: "9"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: f1da933a2ee7c179a55da7d33c61539d440eabc3
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/22/2017
---
# <a name="how-to-paint-an-area-with-a-radial-gradient"></a>Procedura: disegnare un'area con una sfumatura radiale
In questo esempio viene illustrato come utilizzare la <xref:System.Windows.Media.RadialGradientBrush> classe per disegnare un'area con una sfumatura radiale.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene utilizzato un <xref:System.Windows.Media.RadialGradientBrush> per disegnare un rettangolo con una sfumatura radiale che effettua la transizione da giallo a rosso blu per verde limone.  
  
 [!code-csharp[BrushesIntroduction_snip#SimpleRadialGradientExampleWholePage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BrushesIntroduction_snip/CSharp/RadialGradientBrushSnippet.cs#simpleradialgradientexamplewholepage)]
 [!code-vb[BrushesIntroduction_snip#SimpleRadialGradientExampleWholePage](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/BrushesIntroduction_snip/visualbasic/radialgradientbrushsnippet.vb#simpleradialgradientexamplewholepage)]
 [!code-xaml[BrushesIntroduction_snip#SimpleRadialGradientExampleWholePage](../../../../samples/snippets/xaml/VS_Snippets_Wpf/BrushesIntroduction_snip/XAML/RadialGradientBrushSnippet.xaml#simpleradialgradientexamplewholepage)]  
  
 Nella figura seguente viene illustrata la sfumatura dell'esempio precedente. È stata evidenziata della sfumatura.  
  
 ![Cursori sfumatura in una sfumatura radiale](../../../../docs/framework/wpf/graphics-multimedia/media/wcpsdk-graphicsmm-4gradientstops-rg.png "wcpsdk_graphicsmm_4gradientstops_rg")  
  
> [!NOTE]
>  Gli esempi in questo argomento usano il sistema di coordinate per l'impostazione di punti di controllo. Il sistema di coordinate è relativo a un rettangolo di selezione: 0 indica 0 percento del rettangolo di selezione, mentre 1 indica 100% del rettangolo di selezione. È possibile modificare il sistema di coordinate impostando il <xref:System.Windows.Media.GradientBrush.MappingMode%2A> il valore della proprietà <xref:System.Windows.Media.BrushMappingMode.Absolute>. Un sistema di coordinate assoluto non è relativo a un rettangolo di selezione. I valori vengono interpretati direttamente nello spazio locale.  
  
 Per ulteriori <xref:System.Windows.Media.RadialGradientBrush> esempi, vedere il [esempio](http://go.microsoft.com/fwlink/?LinkID=159973). Per ulteriori informazioni sulle sfumature e altri tipi di pennelli, vedere [disegni con colori a tinta unita e sfumature Panoramica](../../../../docs/framework/wpf/graphics-multimedia/painting-with-solid-colors-and-gradients-overview.md).
