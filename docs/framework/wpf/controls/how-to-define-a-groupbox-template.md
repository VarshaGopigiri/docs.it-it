---
title: 'Procedura: definire un modello GroupBox'
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-wpf
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- controls [WPF], GroupBox
- GroupBox control [WPF], creating templates
ms.assetid: 85a4d1a7-4753-4f4a-b26d-14fa10c1ddb5
caps.latest.revision: "9"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 6022f4a521fa64246a24b7aab21c368f5f72af8d
ms.sourcegitcommit: c0dd436f6f8f44dc80dc43b07f6841a00b74b23f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/19/2018
---
# <a name="how-to-define-a-groupbox-template"></a>Procedura: definire un modello GroupBox
In questo esempio viene illustrato come creare un modello per un <xref:System.Windows.Controls.GroupBox> controllo.  
  
## <a name="example"></a>Esempio  
 L'esempio seguente definisce un <xref:System.Windows.Controls.GroupBox> il modello di controllo utilizzando un <xref:System.Windows.Controls.Grid> controllo per il layout. Il modello utilizza un <xref:System.Windows.Controls.BorderGapMaskConverter> per definire il bordo del <xref:System.Windows.Controls.GroupBox> in modo che non nasconda la <xref:System.Windows.Controls.HeaderedContentControl.Header%2A> contenuto.  
  
 [!code-xaml[GroupBoxSnippet#GroupBoxTemplate](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GroupBoxSnippet/CS/Window1.xaml#groupboxtemplate)]  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Windows.Controls.GroupBox>  
 [Procedure relative al controllo GroupBox](http://msdn.microsoft.com/library/7692e155-a4c6-428c-b7e0-64b3740daca7)
