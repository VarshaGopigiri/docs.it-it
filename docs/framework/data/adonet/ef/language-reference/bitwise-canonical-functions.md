---
title: Funzioni canoniche bit per bit
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-ado
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 993868ca-16e3-47b6-9915-c29cd63b0a21
caps.latest.revision: "2"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: dotnet
ms.openlocfilehash: 1d703b2467d508324f3eb39b822c239484ac1c6e
ms.sourcegitcommit: ed26cfef4e18f6d93ab822d8c29f902cff3519d1
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/17/2018
---
# <a name="bitwise-canonical-functions"></a>Funzioni canoniche bit per bit
[!INCLUDE[esql](../../../../../../includes/esql-md.md)] include funzioni canoniche bit per bit.  
  
## <a name="remarks"></a>Note  
 Nella tabella seguente sono illustrate le funzioni canoniche bit per bit [!INCLUDE[esql](../../../../../../includes/esql-md.md)]. Queste funzioni restituiscono `Null` se `Null` viene specificato l'input. Il tipo restituito delle funzioni sarà uguale ai tipi di argomenti. Gli argomenti devono essere dello stesso tipo, se la funzione ne accetta più di uno. Per eseguire operazioni bit per bit tra tipi diversi, è necessario eseguire il cast in modo esplicito lo stesso tipo.  
  
|Funzione|Descrizione|  
|--------------|-----------------|  
|`BitWiseAnd (` `value1` `,`  `value2` `)`|Restituisce la congiunzione bit per bit di `value1` e `value2` come tipo di `value1` e `value2`.<br /><br /> **Argomenti**<br /><br /> Oggetto `Byte`, `Int16`, `Int32`, e `Int64`.<br /><br /> **Esempio**<br /><br /> `-- The following example returns 1.`<br /><br /> `BitWiseAnd(1,3)`|  
|`BitWiseNot (` `value` `)`|Restituisce la negazione bit per bit di `value`.<br /><br /> **Argomenti**<br /><br /> Oggetto `Byte`, `Int16`, `Int32`, e `Int64`.<br /><br /> **Esempio**<br /><br /> `-- The following example returns -4.`<br /><br /> `BitWiseNot(3)`|  
|`BitWiseOr (` `value1` `,`  `value2` `)`|Restituisce la disgiunzione bit per bit di `value1` e `value2` come tipo di `value1` e `value2`.<br /><br /> **Argomenti**<br /><br /> Oggetto `Byte`, `Int16`, `Int32` e `Int64`.<br /><br /> **Esempio**<br /><br /> `-- The following example returns 3.`<br /><br /> `BitWiseOr(1,3)`|  
|`BitWiseXor (` `value1` `,`  `value2` `)`|Restituisce la disgiunzione esclusiva bit per bit di `value1` e `value2` come tipo di `value1` e `value2`.<br /><br /> **Argomenti**<br /><br /> Oggetto `Byte`, `Int16`, `Int32` e `Int64`.<br /><br /> **Esempio**<br /><br /> `-- The following example returns 2.`<br /><br /> `BitWiseXor (1,3)`|  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni canoniche](../../../../../../docs/framework/data/adonet/ef/language-reference/canonical-functions.md)
