---
title: "CStdioFile Class"
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
  - "CStdioFile"
dev_langs: 
  - "C++"
helpviewer_keywords: 
  - "CStdioFile class"
  - "I/O [MFC], stream"
  - "stream I/O"
ms.assetid: 88c2274c-4f0e-4327-882a-557ba4b3ae15
caps.latest.revision: 18
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
# CStdioFile Class
Represents a C run-time stream file as opened by the run-time function [fopen](../crt/fopen--_wfopen.md).  
  
## Syntax  
  
```  
class CStdioFile : public CFile  
```  
  
## Members  
  
### Public Constructors  
  
|Name|Description|  
|----------|-----------------|  
|[CStdioFile::CStdioFile](#cstdiofile__cstdiofile)|Constructs a `CStdioFile` object from a path or file pointer.|  
  
### Public Methods  
  
|Name|Description|  
|----------|-----------------|  
|[CStdioFile::Open](#cstdiofile__open)|Overloaded. Open is designed for use with the default `CStdioFile` constructor (Overrides [CFile::Open](../mfcref/cfile-class.md#cfile__open)).|  
|[CStdioFile::ReadString](#cstdiofile__readstring)|Reads a single line of text.|  
|[CStdioFile::Seek](#cstdiofile__seek)|Positions the current file pointer.|  
|[CStdioFile::WriteString](#cstdiofile__writestring)|Writes a single line of text.|  
  
### Public Data Members  
  
|Name|Description|  
|----------|-----------------|  
|[CStdioFile::m_pStream](#cstdiofile__m_pstream)|Contains a pointer to an open file.|  
  
## Remarks  
 Stream files are buffered and can be opened in either text mode (the default) or binary mode.  
  
 Text mode provides special processing for carriage return–linefeed pairs. When you write a newline character (0x0A) to a text-mode `CStdioFile` object, the byte pair (0x0D, 0x0A) is sent to the file. When you read, the byte pair (0x0D, 0x0A) is translated to a single 0x0A byte.  
  
 The [CFile](../mfcref/cfile-class.md) functions [Duplicate](../mfcref/cfile-class.md#cfile__duplicate), [LockRange](../mfcref/cfile-class.md#cfile__lockrange), and [UnlockRange](../mfcref/cfile-class.md#cfile__unlockrange) are not supported for `CStdioFile`.  
  
 If you call these functions on a `CStdioFile`, you will get a [CNotSupportedException](../mfcref/cnotsupportedexception-class.md).  
  
 For more information on using `CStdioFile`, see the articles [Files in MFC](../mfc/files-in-mfc.md) and [File Handling](../crt/file-handling.md) in the                 *Run-Time Library Reference*.  
  
## Inheritance Hierarchy  
 [CObject](../mfcref/cobject-class.md)  
  
 [CFile](../mfcref/cfile-class.md)  
  
 `CStdioFile`  
  
## Requirements  
 **Header:** afx.h  
  
##  <a name="cstdiofile__cstdiofile"></a>  CStdioFile::CStdioFile  
 Constructs and initializes a `CStdioFile` object.  
  
```  
CStdioFile();  
  
CStdioFile(  
    CAtlTransactionManager* pTM );  
  
CStdioFile(  
    FILE* pOpenStream );  
  
CStdioFile(  
    LPCTSTR lpszFileName,  
    UINT nOpenFlags );  
  
CStdioFile(  
    LPCTSTR lpszFileName, UINT nOpenFlags, CAtlTransactionManager* pTM );  
```  
  
### Parameters  
 `pOpenStream`  
 Specifies the file pointer returned by a call to the C run-time function [fopen](../crt/fopen--_wfopen.md).  
  
 `lpszFileName`  
 Specifies a string that is the path to the desired file. The path can be relative or absolute.  
  
 `nOpenFlags`  
 Specifies options for file creation, file sharing, and file access modes. You can specify multiple options by using the bitwise OR ( `|`) operator.  
  
 One file access mode option is required; other modes are optional. See [CFile::CFile](../mfcref/cfile-class.md#cfile__cfile) for a list of mode options and other flags. In MFC version 3.0 and later, share flags are allowed.  
  
 `pTM`  
 Pointer to CAtlTransactionManager object.  
  
### Remarks  
 The default constructor does not attach a file to the `CStdioFile` object. When using this constructor, you must use the `CStdioFile::Open` method to open a file and attach it to the `CStdioFile` object.  
  
 The single-parameter constructor attaches an open file stream to the `CStdioFile` object. Allowed pointer values include the predefined input/output file pointers `stdin`, `stdout`, or `stderr`.  
  
 The two-parameter constructor creates a `CStdioFile` object and opens the corresponding file with the given path.  
  
 If you pass `NULL` for either `pOpenStream` or `lpszFileName`, the constructor throws a `CInvalidArgException*`.  
  
 If the file cannot be opened or created, the constructor throws a `CFileException*`.  
  
### Example  
 [!code[NVC_MFCFiles#37](../atl/codesnippet/CPP/cstdiofile-class_1.cpp)]  
  
##  <a name="cstdiofile__m_pstream"></a>  CStdioFile::m_pStream  
 The `m_pStream` data member is the pointer to an open file as returned by the C run-time function `fopen`.  
  
```  
FILE* m_pStream;  
```  
  
### Remarks  
 It is **NULL** if the file has never been opened or has been closed.  
  
##  <a name="cstdiofile__open"></a>  CStdioFile::Open  
 Overloaded. Open is designed for use with the default `CStdioFile` constructor.  
  
```  
virtual BOOL Open(  
    LPCTSTR lpszFileName,  
    UINT nOpenFlags,  
    CFileException* pError = NULL);  
  
virtual BOOL Open(  
    LPCTSTR lpszFileName,  
    UINT nOpenFlags,  
    CAtlTransactionManager* pTM,  
    CFileException* pError = NULL);  
```  
  
### Parameters  
 `lpszFileName`  
 A string that is the path to the desired file. The path can be relative or absolute.  
  
 `nOpenFlags`  
 Sharing and access mode. Specifies the action to take when opening the file. You can combine options by using the bitwise-OR (&#124;) operator. One access permission and one share option are required; the modeCreate and modeNoInherit modes are optional.  
  
 `pError`  
 A pointer to an existing file-exception object that will receive the status of a failed operation.  
  
 `pTM`  
 Pointer to a `CAtlTransactionManager` object.  
  
### Return Value  
 `TRUE` if successful; otherwise `FALSE`.  
  
### Remarks  
  
##  <a name="cstdiofile__readstring"></a>  CStdioFile::ReadString  
 Reads text data into a buffer, up to a limit of `nMax`–1 characters, from the file associated with the `CStdioFile` object.  
  
```  
virtual LPTSTR ReadString(  
    LPTSTR lpsz,  
    UINT nMax );  
  
virtual BOOL ReadString(  
    CString& rString );  
```  
  
### Parameters  
 `lpsz`  
 Specifies a pointer to a user-supplied buffer that will receive a null-terminated text string.  
  
 `nMax`  
 Specifies the maximum number of characters to read, not counting the terminating null character.  
  
 `rString`  
 A reference to a `CString` object that will contain the string when the function returns.  
  
### Return Value  
 A pointer to the buffer containing the text data. **NULL** if end-of-file was reached without reading any data; or if boolean, **FALSE** if end-of-file was reached without reading any data.  
  
### Remarks  
 Reading is stopped by the first newline character. If, in that case, fewer than `nMax`–1 characters have been read, a newline character is stored in the buffer. A null character ('\0') is appended in either case.  
  
 [CFile::Read](../mfcref/cfile-class.md#cfile__read) is also available for text-mode input, but it does not terminate on a carriage return–linefeed pair.  
  
> [!NOTE]
>  The `CString` version of this function removes the `'\n'` if present; the `LPTSTR` version does not.  
  
### Example  
 [!code[NVC_MFCFiles#38](../atl/codesnippet/CPP/cstdiofile-class_2.cpp)]  
  
##  <a name="cstdiofile__seek"></a>  CStdioFile::Seek  
 Repositions the pointer in a previously opened file.  
  
```  
virtual ULONGLONG Seek(  
    LONGLONG lOff,  
    UINT nFrom );  
```  
  
### Parameters  
 `lOff`  
 Number of bytes to move the pointer.  
  
 `nFrom`  
 Pointer movement mode. Must be one of the following values:  
  
-   `CFile::begin`: Move the file pointer `lOff` bytes forward from the beginning of the file.  
  
-   `CFile::current`: Move the file pointer `lOff` bytes from the current position in the file.  
  
-   `CFile::end`: Move the file pointer `lOff` bytes from the end of the file. Note that `lOff` must be negative to seek into the existing file; positive values will seek past the end of the file.  
  
### Return Value  
 If the requested position is legal, `Seek` returns the new byte offset from the beginning of the file. Otherwise, the return value is undefined and a `CFileException` object is thrown.  
  
### Remarks  
 The `Seek` function permits random access to a file's contents by moving the pointer a specified amount, absolutely or relatively. No data is actually read during the seek. If the requested position is larger than the size of the file, the file length will be extended to that position, and no exception will be thrown.  
  
 When a file is opened, the file pointer is positioned at offset 0, the beginning of the file.  
  
 This implementation of `Seek` is based on the Run-Time Library (CRT) function `fseek`. There are several limits on the usage of `Seek` on streams opened in text mode. For more information, see [fseek, _fseeki64](../crt/fseek--_fseeki64.md).  
  
### Example  
 The following example shows how to use `Seek` to move the pointer 1000 bytes from the beginning of the `cfile` file. Note that `Seek` does not read data, so you must subsequently call [CStdioFile::ReadString](#cstdiofile__readstring) to read data.  
  
 [!code[NVC_MFCFiles#39](../atl/codesnippet/CPP/cstdiofile-class_3.cpp)]  
  
##  <a name="cstdiofile__writestring"></a>  CStdioFile::WriteString  
 Writes data from a buffer to the file associated with the `CStdioFile` object.  
  
```  
virtual void WriteString( LPCTSTR lpsz );  
```  
  
### Parameters  
 `lpsz`  
 Specifies a pointer to a buffer that contains a null-terminated string.  
  
### Remarks  
 The terminating null character ( `\0`) is not written to the file. This method writes newline characters in `lpsz` to the file as a carriage return/linefeed pair.  
  
 If you want to write data that is not null-terminated to a file, use `CStdioFile::Write` or [CFile::Write](../mfcref/cfile-class.md#cfile__write).  
  
 This method throws a `CInvalidArgException*` if you specify `NULL` for the `lpsz` parameter.  
  
 This method throws a `CFileException*` in response to file system errors.  
  
### Example  
 [!code[NVC_MFCFiles#40](../atl/codesnippet/CPP/cstdiofile-class_4.cpp)]  
  
## See Also  
 [CFile Class](../mfcref/cfile-class.md)   
 [Hierarchy Chart](../mfc/hierarchy-chart.md)   
 [CFile Class](../mfcref/cfile-class.md)   
 [CFile::Duplicate](../mfcref/cfile-class.md#cfile__duplicate)   
 [CFile::LockRange](../mfcref/cfile-class.md#cfile__lockrange)   
 [CFile::UnlockRange](../mfcref/cfile-class.md#cfile__unlockrange)   
 [CNotSupportedException Class](../mfcref/cnotsupportedexception-class.md)   
 [How Do I: Use the CFile Class?](http://go.microsoft.com/fwlink/?LinkId=128046)