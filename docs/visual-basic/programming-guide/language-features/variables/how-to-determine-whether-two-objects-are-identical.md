---
title: 'Procedura: determinare se due oggetti sono identici (Visual Basic)'
ms.custom: 
ms.date: 07/20/2015
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- testing [Visual Basic], objects
- objects [Visual Basic], comparing
- object variables [Visual Basic], determining identity
ms.assetid: 7829f817-0d1f-4749-a707-de0b95e0cf5c
caps.latest.revision: "19"
author: dotnet-bot
ms.author: dotnetcontent
ms.openlocfilehash: 02083a93e63fe799f529776f777ca877d2d138b1
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/21/2017
---
# <a name="how-to-determine-whether-two-objects-are-identical-visual-basic"></a>Procedura: determinare se due oggetti sono identici (Visual Basic)
In [!INCLUDE[vbprvb](~/includes/vbprvb-md.md)], due riferimenti a variabili vengono considerati identici se i relativi puntatori sono uguali, vale a dire se entrambe le variabili puntano alla stessa istanza di classe in memoria. Ad esempio, in un'applicazione Windows Form, è consigliabile eseguire un confronto per determinare se l'istanza corrente (`Me`) è uguale a un'istanza specifica, ad esempio `Form2`.  
  
 [!INCLUDE[vbprvb](~/includes/vbprvb-md.md)]fornisce due operatori per confrontare i puntatori. Il [operatore Is](../../../../visual-basic/language-reference/operators/is-operator.md) restituisce `True` se gli oggetti sono identici e [operatore IsNot](../../../../visual-basic/language-reference/operators/isnot-operator.md) restituisce `True` se non lo sono.  
  
## <a name="determining-if-two-objects-are-identical"></a>Determinare se due oggetti sono identici  
  
#### <a name="to-determine-if-two-objects-are-identical"></a>Per determinare se due oggetti sono identici  
  
1.  Impostare un `Boolean` espressione per testare i due oggetti.  
  
2.  Nell'espressione test, utilizzare il `Is` operatore con i due oggetti come operandi.  
  
     `Is`Restituisce `True` se gli oggetti puntano alla stessa istanza di classe.  
  
## <a name="determining-if-two-objects-are-not-identical"></a>Determinare se due oggetti non sono identici  
 Talvolta si desidera eseguire un'azione, se i due oggetti non sono identici, ma può essere difficile combinare `Not` e `Is`, ad esempio `If Not obj1 Is obj2`. In questo caso è possibile utilizzare il `IsNot` operatore.  
  
#### <a name="to-determine-if-two-objects-are-not-identical"></a>Per determinare se due oggetti non sono identici  
  
1.  Impostare un `Boolean` espressione per testare i due oggetti.  
  
2.  Nell'espressione test, utilizzare il `IsNot` operatore con i due oggetti come operandi.  
  
     `IsNot`Restituisce `True` se gli oggetti non puntano alla stessa istanza di classe.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente verifica coppie di `Object` variabili per stabilire se puntano alla stessa istanza di classe.  
  
 [!code-vb[VbVbalrKeywords#14](../../../../visual-basic/language-reference/codesnippet/VisualBasic/how-to-determine-whether-two-objects-are-identical_1.vb)]  
  
 Nell'esempio precedente viene visualizzato l'output seguente.  
  
 `objA different from objB? True`  
  
 `objA identical to objC? True`  
  
## <a name="see-also"></a>Vedere anche  
 [Tipo di dati Object](../../../../visual-basic/language-reference/data-types/object-data-type.md)  
 [Variabili oggetto](../../../../visual-basic/programming-guide/language-features/variables/object-variables.md)  
 [Valori di variabili oggetto](../../../../visual-basic/programming-guide/language-features/variables/object-variable-values.md)  
 [Operatore Is](../../../../visual-basic/language-reference/operators/is-operator.md)  
 [Operatore IsNot](../../../../visual-basic/language-reference/operators/isnot-operator.md)  
 [Procedura: determinare se due oggetti sono correlati](../../../../visual-basic/programming-guide/language-features/variables/how-to-determine-whether-two-objects-are-related.md)  
 [Me, My, MyBase e MyClass](../../../../visual-basic/programming-guide/program-structure/me-my-mybase-and-myclass.md)
