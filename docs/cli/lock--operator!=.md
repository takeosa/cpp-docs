---
title: "lock::operator!="
ms.custom: na
ms.date: "10/14/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: na
ms.suite: na
ms.technology: 
  - "devlang-cpp"
ms.tgt_pltfrm: na
ms.topic: "reference"
f1_keywords: 
  - "lock.operator!="
  - "msclr.lock.operator!="
  - "msclr::lock::operator!="
  - "lock::operator!="
dev_langs: 
  - "C++"
helpviewer_keywords: 
  - "lock::operator!="
ms.assetid: ed1d674e-9ee9-4257-8a7e-2e3567d50222
caps.latest.revision: 4
ms.author: "mblome"
manager: "ghogen"
translation.priority.ht: 
  - "cs-cz"
  - "de-de"
  - "es-es"
  - "fr-fr"
  - "it-it"
  - "ja-jp"
  - "ko-kr"
  - "pl-pl"
  - "pt-br"
  - "ru-ru"
  - "tr-tr"
  - "zh-cn"
  - "zh-tw"
---
# lock::operator!=
Inequality operator.  
  
## Syntax  
  
```  
template<class T> bool operator!=(  
   T t  
);  
```  
  
#### Parameters  
 `t`  
 The object to compare for inequality.  
  
## Return Value  
 Returns `true` if `t` differs from the lock's object, `false` otherwise.  
  
## Example  
  
```  
// msl_lock_op_ineq.cpp  
// compile with: /clr  
#include <msclr/lock.h>  
  
using namespace System;  
using namespace System::Threading;  
using namespace msclr;  
  
int main () {  
   Object^ o1 = gcnew Object;  
   Object^ o2 = gcnew Object;  
   lock l1(o1);  
   if (l1 != o2) {  
      Console::WriteLine("Inequal!");  
   }  
}  
```  
  
 **Inequal!**   
## Requirements  
 **Header file** \<msclr\lock.h>  
  
 **Namespace** msclr  
  
## See Also  
 [lock Members](../cli/lock-members.md)   
 [lock::operator==](../cli/lock--operator==.md)