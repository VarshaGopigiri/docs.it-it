---
title: private (Riferimenti per C#)
ms.date: 07/20/2015
ms.prod: .net
ms.technology: devlang-csharp
ms.topic: article
f1_keywords:
- private_CSharpKeyword
- private
helpviewer_keywords: private keyword [C#]
ms.assetid: 654c0bb8-e6ac-4086-bf96-7474fa6aa1c8
caps.latest.revision: "17"
author: BillWagner
ms.author: wiwagn
ms.openlocfilehash: d9cc8f86166888b47a758e200182d319c68ca6d4
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/21/2017
---
# <a name="private-c-reference"></a>private (Riferimenti per C#)
La parola chiave `private` è un modificatore di accesso ai membri. 
   
 > Questa pagina illustra `private` accesso. Il `private` parola chiave è anche in parte il [ `private protected` ](./private-protected.md) modificatore di accesso.
  
L'accesso privato è il livello di accesso più restrittivo. I membri privati sono accessibili solo all'interno del corpo della classe o dello struct in cui sono stati dichiarati, come nell'esempio seguente:  
  
```  
class Employee  
{  
    private int i;  
    double d;   // private access by default  
}  
```  

 Anche i tipi annidati dello stesso corpo possono accedere ai membri privati.  
  
 Fare riferimento a un membro privato all'esterno della classe o dello struct in cui è stato dichiarato genera un errore in fase di compilazione.  
  
 Per un confronto di `private` con altri modificatori di accesso, vedere [Livelli di accessibilità](../../../csharp/language-reference/keywords/accessibility-levels.md) e [Modificatori di accesso](../../../csharp/programming-guide/classes-and-structs/access-modifiers.md).  
  
## <a name="example"></a>Esempio  
 In questo esempio la classe `Employee` contiene due membri dati privati, `name` e `salary`. Essendo privati, i membri risulteranno accessibili solo ai metodi di membro. I metodi pubblici `GetName` e `Salary` vengono aggiunti per consentire il controllo dell'accesso ai membri privati. È possibile accedere al membro `name` tramite un metodo pubblico e al membro `salary` tramite una proprietà pubblica di sola lettura. Per altre informazioni, vedere [Proprietà](../../../csharp/programming-guide/classes-and-structs/properties.md).  
  
 [!code-csharp[csrefKeywordsModifiers#10](../../../csharp/language-reference/keywords/codesnippet/CSharp/private_1.cs)]  
  
## <a name="c-language-specification"></a>Specifiche del linguaggio C#  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimenti per C#](../../../csharp/language-reference/index.md)  
 [Guida per programmatori C#](../../../csharp/programming-guide/index.md)  
 [Parole chiave di C#](../../../csharp/language-reference/keywords/index.md)  
 [Modificatori di accesso](../../../csharp/language-reference/keywords/access-modifiers.md)  
 [Livelli di accessibilità](../../../csharp/language-reference/keywords/accessibility-levels.md)  
 [Modificatori](../../../csharp/language-reference/keywords/modifiers.md)  
 [public](../../../csharp/language-reference/keywords/public.md)  
 [protected](../../../csharp/language-reference/keywords/protected.md)  
 [internal](../../../csharp/language-reference/keywords/internal.md)
