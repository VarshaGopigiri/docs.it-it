---
title: 'Procedura: associare un controllo ListBox ai dati'
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-wpf
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ListBox controls [WPF], binding data to
- data binding [WPF], ListBox control
- binding data [WPF], to ListBox control
ms.assetid: de93a907-709a-44a7-84bf-578b846a3d8b
caps.latest.revision: "12"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: a4701fe99231e115eb8cb14f7c1e5e003928bc5e
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/22/2017
---
# <a name="how-to-bind-a-listbox-to-data"></a>Procedura: associare un controllo ListBox ai dati
Uno sviluppatore di applicazioni può creare <xref:System.Windows.Controls.ListBox> controlli senza specificare il contenuto di ciascuna <xref:System.Windows.Controls.ListBoxItem> separatamente. È possibile utilizzare l'associazione dati per associare i dati per i singoli elementi.  
  
 Nell'esempio seguente viene illustrato come creare un <xref:System.Windows.Controls.ListBox> che popola la <xref:System.Windows.Controls.ListBoxItem> elementi utilizzando l'associazione dati a un'origine dati denominata *colori*. In questo caso non è necessario utilizzare <xref:System.Windows.Controls.ListBoxItem> tag per specificare il contenuto di ogni elemento.  
  
## <a name="example"></a>Esempio  
 [!code-xaml[ListBoxEvent#7](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ListBoxEvent/CSharp/Pane1.xaml#7)]  
[!code-xaml[ListBoxEvent#3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ListBoxEvent/CSharp/Pane1.xaml#3)]  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Windows.Controls.ListBox>  
 <xref:System.Windows.Controls.ListBoxItem>  
 [Controlli](../../../../docs/framework/wpf/advanced/optimizing-performance-controls.md)
