---
title: Impossibile dedurre da questi argomenti i tipi di dati dei parametri di tipo
ms.date: 07/20/2015
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: devlang-visual-basic
ms.topic: article
f1_keywords:
- bc36644
- bc36647
- vbc36647
- vbc36644
helpviewer_keywords:
- BC36644
- BC36647
ms.assetid: 0e0050f2-2039-4311-b260-f0ebfde84189
caps.latest.revision: "6"
author: dotnet-bot
ms.author: dotnetcontent
ms.openlocfilehash: b290c25286dce2236823919e8287db9abefc0dd7
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/21/2017
---
# <a name="data-types-of-the-type-parameters-cannot-be-inferred-from-these-arguments"></a>Impossibile dedurre da questi argomenti i tipi di dati dei parametri di tipo
Impossibile dedurre da questi argomenti i tipi di dati dei parametri di tipo. Per correggere l'errore, provare a specificare i tipi di dati in modo esplicito.  
  
 Questo errore si verifica quando la risoluzione dell'overload non riesce. Viene visualizzato come messaggio subordinato che indica perché un determinato candidato di overload è stato eliminato. Il messaggio di errore spiega che il compilatore non è possibile usare l'inferenza del tipo per trovare tipi di dati per i parametri di tipo.  
  
> [!NOTE]
>  Quando non è possibile specificare gli argomenti (ad esempio per gli operatori di query nelle espressioni di query), il messaggio di errore visualizzato non contiene la seconda frase.  
  
 Il codice seguente illustra l'errore.  
  
```vb  
Module Module1  
  
    Sub Main()  
  
        '' Not Valid.  
        'OverloadedGenericMethod("Hello", "World")  
  
    End Sub  
  
    Sub OverloadedGenericMethod(Of T)(ByVal x As String,   
                                      ByVal y As InterfaceExample(Of T))  
    End Sub  
  
    Sub OverloadedGenericMethod(Of T, R)(ByVal x As T,   
                                         ByVal y As InterfaceExample(Of R))  
    End Sub  
  
End Module  
  
Interface InterfaceExample(Of T)  
End Interface  
```  
  
 **ID errore:** BC36647 e BC36644  
  
## <a name="to-correct-this-error"></a>Per correggere l'errore  
  
-   È possibile specificare un tipo di dati per il parametro o i parametri di tipo anziché basarsi sull'inferenza del tipo.  
  
## <a name="see-also"></a>Vedere anche  
 [Conversione di tipo relaxed del delegato](../../../visual-basic/programming-guide/language-features/delegates/relaxed-delegate-conversion.md)  
 [Routine generiche in Visual Basic](../../../visual-basic/programming-guide/language-features/data-types/generic-procedures.md)  
 [Conversioni di tipi in Visual Basic](../../../visual-basic/programming-guide/language-features/data-types/type-conversions.md)
