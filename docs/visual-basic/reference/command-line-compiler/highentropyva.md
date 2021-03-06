---
title: /highentropyva (Visual Basic)
ms.date: 07/20/2015
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: devlang-visual-basic
ms.topic: article
helpviewer_keywords:
- highentropyva compiler option (Visual Basic)
- /highentropyva compiler option (Visual Basic)
ms.assetid: ff25f20a-6ca2-467b-9e52-5cf439f5028e
caps.latest.revision: "12"
author: dotnet-bot
ms.author: dotnetcontent
ms.openlocfilehash: 55568808bb94f98ce7a20016fc5a2a0a2ef23a38
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/21/2017
---
# <a name="highentropyva-visual-basic"></a>/highentropyva (Visual Basic)
Indica se un eseguibile a 64 bit o che è stata contrassegnata dal [/platform: anycpu](../../../visual-basic/reference/command-line-compiler/platform.md) supporta l'opzione del compilatore Address Space Layout Randomization (ASLR) a entropia elevata.  
  
## <a name="syntax"></a>Sintassi  
  
```  
/highentropyva[+ | -]  
```  
  
## <a name="arguments"></a>Argomenti  
 `+` &#124; `-`  
 Parametro facoltativo. L'opzione è disattivata per impostazione predefinita o se si specifica `/highentropyva-`. L'opzione è abilitata se si specifica `/highentropyva` o `/highentropyva+`.  
  
## <a name="remarks"></a>Note  
 Se si specifica questa opzione, le versioni compatibili del kernel di Windows consente un grado più elevato di entropia quando il kernel genera casualmente il layout dello spazio degli indirizzi di un processo come parte di ASLR. Se il kernel utilizza un grado più elevato di entropia, un numero maggiore di indirizzi può essere allocato alle aree di memoria quali stack e heap. Di conseguenza, è più difficile indovinare la posizione di una determinata area di memoria.  
  
 Quando l'opzione è on, l'eseguibile di destinazione e tutti i moduli in cui esso dipende deve essere in grado di gestire i valori dei puntatori sono maggiori di 4 gigabyte (GB) quando i moduli vengono eseguiti come processi a 64 bit.  
  
## <a name="see-also"></a>Vedere anche  
 [Compilatore della riga di comando di Visual Basic](../../../visual-basic/reference/command-line-compiler/index.md)  
 [Esempi di righe di comando di compilazione](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
