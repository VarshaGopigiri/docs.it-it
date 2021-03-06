---
title: Funzioni locali (Guida per programmatori C#)
ms.date: 06/14/2017
ms.prod: .net
ms.technology: devlang-csharp
ms.topic: article
helpviewer_keywords: local functions [C#]
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 2b4e95d48e451038f0f7004d0901f329b2c57fe5
ms.sourcegitcommit: 7e99f66ef09d2903e22c789c67ff5a10aa953b2f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/18/2017
---
# <a name="local-functions-c-programming-guide"></a>Funzioni locali (Guida per programmatori C#)

A partire da C# 7, C# supporta le *funzioni locali*. Le funzioni locali sono metodi privati di un tipo annidati in un altro membro. Possono essere chiamate solo dal relativo membro contenitore. Le funzioni locali, in particolare, possono essere dichiarate in e chiamate da:

- Metodi, soprattutto metodi iteratori e metodi asincroni
- Costruttori
- Funzioni di accesso alle proprietà
- Funzioni di accesso agli eventi
- Metodi anonimi
- Espressioni lambda
- Finalizzatori
- Altre funzioni locali

Le funzioni locali, tuttavia, non possono essere dichiarate all'interno di un membro con corpo di espressione.

> [!NOTE]
> In alcuni casi, è possibile usare un'espressione lambda per implementare le funzionalità supportate anche da una funzione locale. Per un confronto, vedere [Confronto tra funzioni locali ed espressioni Lambda](../../local-functions-vs-lambdas.md).

Le funzioni locali rendono chiaro l'obiettivo del codice. Chiunque legga il codice, ad esempio, può vedere che il metodo può essere chiamato solo dal metodo contenitore. Per i progetti in team, le funzioni locali impediscono anche a un altro sviluppatore di chiamare per errore il metodo direttamente da un altro punto della classe o dello struct.
 
## <a name="local-function-syntax"></a>Sintassi delle funzioni locali

Una funzione locale viene definita come metodo annidato all'interno di un membro contenitore. La definizione presenta la sintassi seguente:

```txt
<modifiers: async | unsafe> <return-type> <method-name> <parameter-list>
```

Le funzioni locali possono usare i modificatori [async](../../language-reference/keywords/async.md) e [unsafe](../../language-reference/keywords/unsafe.md). 

Tutte le variabili locali definite nel membro contenitore, inclusi i relativi parametri di metodo, sono accessibili nella funzione locale. 

Contrariamente a una definizione di metodo, una definizione di funzione locale non può contenere gli elementi seguenti:

- Il modificatore di accesso ai membri. Poiché tutte le funzioni locali sono private, l'integrazione di un modificatore di accesso come la parola chiave `private` genera l'errore del compilatore CS0106: "Il modificatore 'private' non è valido per questo elemento".
 
- La parola chiave [static](../../language-reference/keywords/static.md). L'integrazione della parola chiave `static` genera l'errore del compilatore CS0106: "Il modificatore 'private' non è valido per questo elemento".

Non è possibile, inoltre, applicare attributi alla funzione locale o ai relativi parametri e parametri di tipo. 
 
L'esempio seguente definisce una funzione locale denominata `AppendPathSeparator`, privata di un metodo denominato `GetText`:
   
[!code-csharp[LocalFunctionExample](../../../../samples/snippets/csharp/programming-guide/classes-and-structs/local-functions1.cs)]  
   
## <a name="local-functions-and-exceptions"></a>Funzioni locali ed eccezioni

Le funzioni locali offrono il vantaggio di consentire alle eccezioni di essere rilevate immediatamente. Nel caso degli iteratori di metodo, le eccezioni vengono rilevate solo nel momento in cui la sequenza restituita viene enumerata e non quando viene recuperato l'iteratore. Nel caso dei metodi asincroni, qualsiasi eccezione generata viene rilevata mentre è attesa l'attività restituita. 

L'esempio seguente definisce un metodo `OddSequence` che enumera i numeri dispari in un intervallo specifico. Poiché al metodo enumeratore `OddSequence` viene trasmesso un numero maggiore di 100, il metodo genera una <xref:System.ArgumentOutOfRangeException>. Come illustrato dall'output dell'esempio, l'eccezione viene rilevata solo nel momento in cui vengono iterati i numeri e non quando si recupera l'enumeratore.

[!code-csharp[LocalFunctionIterator1](../../../../samples/snippets/csharp/programming-guide/classes-and-structs/local-functions-iterator1.cs)] 

È possibile tuttavia generare un'eccezione mentre si esegue la convalida e prima di recuperare l'iteratore restituendo l'iteratore da una funzione locale, come illustrato nell'esempio seguente.

[!code-csharp[LocalFunctionIterator2](../../../../samples/snippets/csharp/programming-guide/classes-and-structs/local-functions-iterator2.cs)]

Le funzioni locali possono essere usate in modo analogo anche per gestire eccezioni esterne all'operazione asincrona. In genere, le eccezioni generate in un metodo asincrono richiedono che vengano esaminate le eccezioni interne di una <xref:System.AggregateException>. Le funzioni locali consentono al codice di adottare un approccio "fail fast" e alle eccezioni di essere generate e osservate in modo sincrono.

Nell'esempio seguente viene usato un metodo asincrono denominato `GetMultipleAsync` per sospendere l'operazione per un determinato numero di secondi e restituire un valore che sia un multiplo casuale del numero di secondi specificato. Il ritardo massimo consentito è 5 secondi. Se il valore è superiore a 5, viene generata una <xref:System.ArgumentOutOfRangeException>. Come illustrato nell'esempio seguente, l'eccezione generata quando al metodo `GetMultipleAsync` viene passato il valore 6 viene sottoposta a wrapping in una <xref:System.AggregateException> dopo che il metodo `GetMultipleAsync` inizia l'esecuzione.

[!code-csharp[LocalFunctionAsync`](../../../../samples/snippets/csharp/programming-guide/classes-and-structs/local-functions-async1.cs)] 

Come per l'iteratore di metodo, è possibile effettuare il refactoring del codice dell'esempio per eseguire la convalida prima di chiamare il metodo asincrono. Come illustrato dall'output dell'esempio seguente, <xref:System.ArgumentOutOfRangeException> non è stata sottoposta a wrapping in una <x:System.AggregateException>.

[!code-csharp[LocalFunctionAsync`](../../../../samples/snippets/csharp/programming-guide/classes-and-structs/local-functions-async2.cs)] 

## <a name="see-also"></a>Vedere anche
[Metodi](methods.md)
