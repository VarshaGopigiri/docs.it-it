---
title: 'Procedura: selezionare l''input penna da un controllo personalizzato'
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
- controls [WPF], ink selection
- ink [WPF], selecting from custom control
- custom controls [WPF], ink selection
ms.assetid: 5f3a45c6-6d40-4017-9b47-933f134ceba3
caps.latest.revision: "5"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 972ece6964d1f3cc42c6221c3b18336e3353bc18
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/22/2017
---
# <a name="how-to-select-ink-from-a-custom-control"></a>Procedura: selezionare l'input penna da un controllo personalizzato
Aggiungendo un <xref:System.Windows.Ink.IncrementalLassoHitTester> al controllo personalizzato, è possibile abilitare il controllo in modo che un utente può selezionare input penna con lo strumento, analogamente al modo in cui il <xref:System.Windows.Controls.InkCanvas> seleziona input penna con un lazo.  
  
 In questo esempio si presuppone che si ha familiarità con la creazione di un controllo personalizzato abilitato input penna.  Per creare un controllo personalizzato che accetta l'input penna, vedere [la creazione di un controllo di Input penna](../../../../docs/framework/wpf/advanced/creating-an-ink-input-control.md).  
  
## <a name="example"></a>Esempio  
 Quando l'utente utilizza lo strumento lazo, il <xref:System.Windows.Ink.IncrementalLassoHitTester> consente di stimare quali tratti sarà all'interno dei confini del lazo lazo al termine dell'operazione.  I tratti che sono determinati all'interno dei confini del lazo possono essere considerati come selezionato.  Tratti selezionati possono anche essere deselezionati.  Se l'utente cambia direzione mentre lazo, ad esempio il <xref:System.Windows.Ink.IncrementalLassoHitTester> deselezione di alcuni tratti.  
  
 Il <xref:System.Windows.Ink.IncrementalLassoHitTester> genera il <xref:System.Windows.Ink.IncrementalLassoHitTester.SelectionChanged> evento, che consente di rispondere mentre l'utente è lazo un controllo personalizzato.  Ad esempio, è possibile modificare l'aspetto dei tratti come utente selezionati e deselezionati.  
  
## <a name="managing-the-ink-mode"></a>Gestione della modalità di input penna  
 È utile per l'utente se il lazo sia diverso rispetto all'input penna sul controllo. A tale scopo, il controllo personalizzato deve tenere traccia di se l'utente è la scrittura o la selezione di input penna. Il modo più semplice per eseguire questa operazione consiste nel dichiarare un'enumerazione con due valori: una per indicare che l'utente scrive input penna e uno per indicare che l'utente seleziona l'input penna.  
  
 [!code-csharp[HowToSelectInk#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HowToSelectInk/CSharp/InkSelector.cs#2)]
 [!code-vb[HowToSelectInk#2](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/HowToSelectInk/VisualBasic/InkSelector.vb#2)]  
  
 Successivamente, aggiungere due <xref:System.Windows.Ink.DrawingAttributes> alla classe: utilizzare quando l'utente scrive input penna, uno da utilizzare quando l'utente seleziona l'input penna.  Nel costruttore, inizializzare il <xref:System.Windows.Ink.DrawingAttributes> e collegare entrambi <xref:System.Windows.Ink.DrawingAttributes.AttributeChanged> eventi al gestore dell'evento stesso. Impostare quindi la <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer.DrawingAttributes%2A> proprietà del <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> all'input penna <xref:System.Windows.Ink.DrawingAttributes>.  
  
 [!code-csharp[HowToSelectInk#3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HowToSelectInk/CSharp/InkSelector.cs#3)]
 [!code-vb[HowToSelectInk#3](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/HowToSelectInk/VisualBasic/InkSelector.vb#3)]  
[!code-csharp[HowToSelectInk#4](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HowToSelectInk/CSharp/InkSelector.cs#4)]
[!code-vb[HowToSelectInk#4](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/HowToSelectInk/VisualBasic/InkSelector.vb#4)]  
  
 Aggiungere una proprietà che espone la modalità di selezione. Quando l'utente modifica la modalità di selezione, impostare il <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer.DrawingAttributes%2A> proprietà del <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> appropriati <xref:System.Windows.Ink.DrawingAttributes> dell'oggetto e quindi ricollegare il <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer.RootVisual%2A> proprietà per il <xref:System.Windows.Controls.InkPresenter>.  
  
 [!code-csharp[HowToSelectInk#5](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HowToSelectInk/CSharp/InkSelector.cs#5)]
 [!code-vb[HowToSelectInk#5](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/HowToSelectInk/VisualBasic/InkSelector.vb#5)]  
  
 Esporre il <xref:System.Windows.Ink.DrawingAttributes> come proprietà affinché le applicazioni possono determinare l'aspetto dei tratti input penna e selezione.  
  
 [!code-csharp[HowToSelectInk#6](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HowToSelectInk/CSharp/InkSelector.cs#6)]
 [!code-vb[HowToSelectInk#6](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/HowToSelectInk/VisualBasic/InkSelector.vb#6)]  
  
 Quando una proprietà di un <xref:System.Windows.Ink.DrawingAttributes> oggetto viene modificato, il <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer.RootVisual%2A> devono essere ricollegate al <xref:System.Windows.Controls.InkPresenter>.  Nel gestore eventi per il <xref:System.Windows.Ink.DrawingAttributes.AttributeChanged> evento, ricollegare il <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer.RootVisual%2A> per il <xref:System.Windows.Controls.InkPresenter>.  
  
 [!code-csharp[HowToSelectInk#7](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HowToSelectInk/CSharp/InkSelector.cs#7)]
 [!code-vb[HowToSelectInk#7](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/HowToSelectInk/VisualBasic/InkSelector.vb#7)]  
  
## <a name="using-the-incrementallassohittester"></a>Utilizzo di IncrementalLassoHitTester  
 Creare e inizializzare un <xref:System.Windows.Ink.StrokeCollection> che contiene i tratti selezionati.  
  
 [!code-csharp[HowToSelectInk#8](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HowToSelectInk/CSharp/InkSelector.cs#8)]
 [!code-vb[HowToSelectInk#8](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/HowToSelectInk/VisualBasic/InkSelector.vb#8)]  
  
 Quando l'utente inizia a disegnare un tratto, input penna o lazo, deselezionare tutte le tracce selezionate. Se l'utente disegna un lazo, creare un <xref:System.Windows.Ink.IncrementalLassoHitTester> chiamando <xref:System.Windows.Ink.StrokeCollection.GetIncrementalLassoHitTester%2A>, sottoscrivere il <xref:System.Windows.Ink.IncrementalLassoHitTester.SelectionChanged> evento e chiamare <xref:System.Windows.Ink.IncrementalHitTester.AddPoints%2A>. Questo codice può essere un metodo separato e chiamata dal <xref:System.Windows.UIElement.OnStylusDown%2A> e <xref:System.Windows.UIElement.OnMouseDown%2A> metodi.  
  
 [!code-csharp[HowToSelectInk#9](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HowToSelectInk/CSharp/InkSelector.cs#9)]
 [!code-vb[HowToSelectInk#9](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/HowToSelectInk/VisualBasic/InkSelector.vb#9)]  
  
 Aggiungere i punti dello stilo per il <xref:System.Windows.Ink.IncrementalLassoHitTester> mentre l'utente disegna il lazo.  Chiamare il metodo seguente dal <xref:System.Windows.UIElement.OnStylusMove%2A>, <xref:System.Windows.UIElement.OnStylusUp%2A>, <xref:System.Windows.UIElement.OnMouseMove%2A>, e <xref:System.Windows.UIElement.OnMouseLeftButtonUp%2A> metodi.  
  
 [!code-csharp[HowToSelectInk#10](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HowToSelectInk/CSharp/InkSelector.cs#10)]
 [!code-vb[HowToSelectInk#10](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/HowToSelectInk/VisualBasic/InkSelector.vb#10)]  
  
 Gestire il <xref:System.Windows.Ink.IncrementalLassoHitTester.SelectionChanged?displayProperty=nameWithType> rispondere quando l'utente seleziona e deseleziona tratti dell'evento.  Il <xref:System.Windows.Ink.LassoSelectionChangedEventArgs> classe dispone di <xref:System.Windows.Ink.LassoSelectionChangedEventArgs.SelectedStrokes%2A> e <xref:System.Windows.Ink.LassoSelectionChangedEventArgs.DeselectedStrokes%2A> proprietà che recuperano i tratti che sono state selezionate e deselezionate, rispettivamente.  
  
 [!code-csharp[HowToSelectInk#11](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HowToSelectInk/CSharp/InkSelector.cs#11)]
 [!code-vb[HowToSelectInk#11](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/HowToSelectInk/VisualBasic/InkSelector.vb#11)]  
  
 Quando l'utente termina di lazo, annullare la sottoscrizione di <xref:System.Windows.Ink.IncrementalLassoHitTester.SelectionChanged> eventi e chiamate <xref:System.Windows.Ink.IncrementalHitTester.EndHitTesting%2A>.  
  
 [!code-csharp[HowToSelectInk#12](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HowToSelectInk/CSharp/InkSelector.cs#12)]
 [!code-vb[HowToSelectInk#12](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/HowToSelectInk/VisualBasic/InkSelector.vb#12)]  
  
## <a name="putting-it-all-together"></a>Inserire tutti insieme.  
 Nell'esempio seguente è un controllo personalizzato che consente all'utente di selezionare input penna con un lazo.  
  
 [!code-csharp[HowToSelectInk#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HowToSelectInk/CSharp/InkSelector.cs#1)]
 [!code-vb[HowToSelectInk#1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/HowToSelectInk/VisualBasic/InkSelector.vb#1)]  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Windows.Ink.IncrementalLassoHitTester>  
 <xref:System.Windows.Ink.StrokeCollection>  
 <xref:System.Windows.Input.StylusPointCollection>  
 [Creazione di un controllo di input penna](../../../../docs/framework/wpf/advanced/creating-an-ink-input-control.md)
