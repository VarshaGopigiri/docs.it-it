---
title: 'Procedura: caricare file nel controllo RichTextBox Windows Form'
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-winforms
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- text boxes [Windows Forms], displaying files
- examples [Windows Forms], text boxes
- .rtf files [Windows Forms], opening in RichTextBox control
- RTF files [Windows Forms], opening in RichTextBox control
- text files [Windows Forms], displaying in RichTextBox control
- .rtf files [Windows Forms], displaying in RichTextBox control
- RichTextBox control [Windows Forms], opening files
- RTF files [Windows Forms], displaying in RichTextBox control
ms.assetid: c03451be-f285-4428-a71a-c41e002cc919
caps.latest.revision: "13"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 003770e5d21383973946c4ebb83d560f0fa23207
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/22/2017
---
# <a name="how-to-load-files-into-the-windows-forms-richtextbox-control"></a>Procedura: caricare file nel controllo RichTextBox Windows Form
Il controllo <xref:System.Windows.Forms.RichTextBox> Windows Form consente di visualizzare un file come testo normale, testo normale Unicode o in formato RTF (Rich-Text Format). Per eseguire questa operazione, chiamare il metodo <xref:System.Windows.Forms.RichTextBox.LoadFile%2A> . È anche possibile usare <xref:System.Windows.Forms.RichTextBox.LoadFile%2A> per caricare dati da un flusso. Per altre informazioni, vedere <xref:System.Windows.Forms.RichTextBox.LoadFile%28System.IO.Stream%2CSystem.Windows.Forms.RichTextBoxStreamType%29>.  
  
### <a name="to-load-a-file-into-the-richtextbox-control"></a>Per caricare un file nel controllo RichTextBox  
  
1.  Determinare il percorso del file da aprire usando il componente <xref:System.Windows.Forms.OpenFileDialog> . Per una panoramica, vedere [Cenni preliminari sul componente OpenFileDialog](../../../../docs/framework/winforms/controls/openfiledialog-component-overview-windows-forms.md).  
  
2.  Chiamare il metodo <xref:System.Windows.Forms.RichTextBox.LoadFile%2A> <xref:System.Windows.Forms.RichTextBox> specificando il file da caricare e, facoltativamente, un tipo di file. Nell'esempio seguente il file da caricare viene preso dalla proprietà <xref:System.Windows.Forms.OpenFileDialog> del componente <xref:System.Windows.Forms.FileDialog.FileName%2A> . Se si chiama il metodo usando come unico argomento un nome di file, si presuppone che il tipo del file sia RTF. Per specificare un altro tipo di file, chiamare il metodo con un valore dell'enumerazione <xref:System.Windows.Forms.RichTextBoxStreamType> come secondo argomento.  
  
     Nell'esempio seguente viene visualizzato il componente <xref:System.Windows.Forms.OpenFileDialog> quando si fa clic su un pulsante. Il file selezionato viene quindi aperto e visualizzato nel controllo <xref:System.Windows.Forms.RichTextBox> . In questo esempio si presuppone l'esistenza di un form contenente un pulsante `btnOpenFile`.  
  
    ```vb  
    Private Sub btnOpenFile_Click(ByVal sender As System.Object, _  
       ByVal e As System.EventArgs) Handles btnOpenFile.Click  
         If OpenFileDialog1.ShowDialog() = DialogResult.OK Then  
           RichTextBox1.LoadFile(OpenFileDialog1.FileName, _  
              RichTextBoxStreamType.RichText)  
          End If  
    End Sub  
    ```  
  
    ```csharp  
    private void btnOpenFile_Click(object sender, System.EventArgs e)  
    {  
       if(openFileDialog1.ShowDialog() == DialogResult.OK)  
       {  
         richTextBox1.LoadFile(openFileDialog1.FileName, RichTextBoxStreamType.RichText);  
       }  
    }  
    ```  
  
    ```cpp  
    private:  
       void btnOpenFile_Click(System::Object ^  sender,  
          System::EventArgs ^  e)  
       {  
          if(openFileDialog1->ShowDialog() == DialogResult::OK)  
          {  
             richTextBox1->LoadFile(openFileDialog1->FileName,  
                RichTextBoxStreamType::RichText);  
          }  
       }  
    ```  
  
     ([!INCLUDE[csprcs](../../../../includes/csprcs-md.md)]e [!INCLUDE[vcprvc](../../../../includes/vcprvc-md.md)]) Inserire il codice seguente nel costruttore del form per registrare il gestore eventi.  
  
    ```csharp  
    this.btnOpenFile.Click += new System.EventHandler(this. btnOpenFile_Click);  
    ```  
  
    ```cpp  
    this->btnOpenFile->Click += gcnew   
       System::EventHandler(this, &Form1::btnOpenFile_Click);  
    ```  
  
    > [!IMPORTANT]
    >  Per eseguire questo processo, l'assembly può richiede un livello di privilegio concesso dalla classe <xref:System.Security.Permissions.FileIOPermission?displayProperty=nameWithType>. Se l'esecuzione avviene in un contesto parzialmente attendibile, è possibile che il processo generi un'eccezione dovuta a privilegi insufficienti. Per altre informazioni, vedere [Code Access Security Basics](../../../../docs/framework/misc/code-access-security-basics.md) (Nozioni di base sulla sicurezza dell'accesso di codice).  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Windows.Forms.RichTextBox.LoadFile%2A?displayProperty=nameWithType>  
 <xref:System.Windows.Forms.RichTextBox>  
 [Controllo RichTextBox](../../../../docs/framework/winforms/controls/richtextbox-control-windows-forms.md)  
 [Controlli da usare in Windows Form](../../../../docs/framework/winforms/controls/controls-to-use-on-windows-forms.md)
