---
title: "Procedura: Registrare una proprietà associata"
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
- attached properties [WPF], registering
- registering attached properties [WPF]
ms.assetid: eb47bd94-0451-4f8d-8fb6-95f7812ac05b
caps.latest.revision: "12"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 37c727eee7b56473808fec06ea42044fc742f7f2
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/22/2017
---
# <a name="how-to-register-an-attached-property"></a>Procedura: Registrare una proprietà associata
Questo esempio mostra come registrare una proprietà associata e fornire funzioni di accesso pubbliche, in modo da poter usare la proprietà sia in [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] che nel codice. Le proprietà associate rappresentano un concetto della sintassi definito da [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]. La maggior parte delle proprietà associate per i tipi [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] viene anche implementata come proprietà di dipendenza. È possibile utilizzare le proprietà di dipendenza in qualsiasi <xref:System.Windows.DependencyObject> tipi.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene illustrato come registrare una proprietà associata come proprietà di dipendenza, tramite il <xref:System.Windows.DependencyProperty.RegisterAttached%2A> metodo. La classe del provider può fornire metadati predefiniti per la proprietà applicabile quando la proprietà viene usata in un'altra classe, a meno che tale classe non esegua l'override dei metadati. In questo esempio il valore predefinito della proprietà `IsBubbleSource` viene impostato su `false`.  
  
 La classe del provider per una proprietà associata (anche se non è registrata come proprietà di dipendenza) deve fornire funzioni di accesso get e set statiche basate sulla convenzione di denominazione `Set`*[NomeProprietàAssociata]* e `Get`*[NomeProprietàAssociata]*. Queste funzioni di accesso sono necessarie per consentire al lettore [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] in funzione di riconoscere la proprietà come attributo in [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] e risolvere i tipi appropriati.  
  
 [!code-csharp[WPFAquariumSln#RegisterAttachedBubbler](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WPFAquariumSln/CSharp/WPFAquariumObjects/Class1.cs#registerattachedbubbler)]
 [!code-vb[WPFAquariumSln#RegisterAttachedBubbler](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WPFAquariumSln/visualbasic/wpfaquariumobjects/class1.vb#registerattachedbubbler)]  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Windows.DependencyProperty>  
 [Panoramica sulle proprietà di dipendenza](../../../../docs/framework/wpf/advanced/dependency-properties-overview.md)  
 [Proprietà di dipendenza personalizzate](../../../../docs/framework/wpf/advanced/custom-dependency-properties.md)  
 [Procedure relative alle proprietà](../../../../docs/framework/wpf/advanced/properties-how-to-topics.md)
