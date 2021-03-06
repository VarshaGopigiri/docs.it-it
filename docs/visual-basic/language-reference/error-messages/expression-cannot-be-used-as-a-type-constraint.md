---
title: "&#39; &lt;espressione&gt;&#39; non può essere utilizzato come vincolo di tipo"
ms.date: 07/20/2015
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: devlang-visual-basic
ms.topic: article
f1_keywords:
- bc32061
- vbc32061
helpviewer_keywords: BC32061
ms.assetid: b17821b7-fa14-4397-a211-6e2a14079f09
caps.latest.revision: "18"
author: dotnet-bot
ms.author: dotnetcontent
ms.openlocfilehash: c7271018a93c97ed90dc272f7f5404c0f0a22d42
ms.sourcegitcommit: 34ec7753acf76f90a0fa845235ef06663dc9e36e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/21/2017
---
# <a name="39ltexpressiongt39-cannot-be-used-as-a-type-constraint"></a>&#39; &lt;espressione&gt;&#39; non può essere utilizzato come vincolo di tipo
Un elenco di vincoli comprende un'espressione che non rappresenta un vincolo valido per un parametro di tipo.  
  
 Un elenco di vincoli impone requisiti per l'argomento di tipo passato al parametro di tipo. Si possono specificare i requisiti seguenti in qualsiasi combinazione:  
  
-   L'argomento di tipo deve implementare una o più interfacce  
  
-   L'argomento di tipo deve ereditare al massimo da una classe  
  
-   L'argomento di tipo deve esporre un costruttore senza parametri a cui il codice di creazione possa accedere (includere il vincolo `New` )  
  
 Se non si include alcuna classe o interfaccia specifica nell'elenco di vincoli, è possibile imporre un requisito più generale specificando una delle condizioni seguenti:  
  
-   L'argomento di tipo deve essere un tipo valore (includere il vincolo `Structure` )  
  
-   L'argomento di tipo deve essere un tipo riferimento (includere il vincolo `Class` )  
  
 Non è possibile specificare sia `Structure` che `Class` per lo stesso parametro di tipo e non è possibile specificare uno dei due vincoli più volte.  
  
 **ID errore:** BC32061  
  
## <a name="to-correct-this-error"></a>Per correggere l'errore  
  
-   Verificare che l'espressione e i suoi elementi siano digitati correttamente.  
  
-   Se l'espressione non soddisfa l'elenco di requisiti precedente, rimuoverla dall'elenco di vincoli.  
  
-   Se l'espressione fa riferimento a un'interfaccia o a una classe, verificare che il compilatore possa accedere a quell'interfaccia o a quella classe. Potrebbe essere necessario qualificarne il nome e anche aggiungere un riferimento al progetto. Per ulteriori informazioni, vedere "Riferimenti ai progetti" in [riferimenti a elementi dichiarati](../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Tipi generici in Visual Basic](../../../visual-basic/programming-guide/language-features/data-types/generic-types.md)  
 [Tipi valore e tipi riferimento](../../../visual-basic/programming-guide/language-features/data-types/value-types-and-reference-types.md)  
 [Riferimenti a elementi dichiarati](../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)  
 
