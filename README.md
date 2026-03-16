# OurC-Syntax-Checker-Pretty-Printer-Built-in-Function-Support

### OurC Interpreter: Syntax Checker & Pretty Printer
## 📝 專案簡介 (Project Overview)
本專案實作了一個 OurC 語言(c-like)的編譯器前端系統。透過手寫的詞法分析器（Lexer）與語法分析器（Parser），系統能夠辨識特定的程式語法、檢測多種層級的錯誤，並將程式碼重新格式化（Pretty Printing）輸出。


## 🚀 核心技術實作 (Technical Implementation)
手寫遞迴下降解析器 (Recursive Descent Parser)：

未使用 Lex/Yacc 工具，完全採用 C++ 實作 GetToken() 與 Scanner 邏輯。

利用 vector<string> gTBuffer 建立 Token 緩衝區，並透過 gCur 指標精準控制解析進度。

Error Handling：

    詞法層級 (Lexical)：辨識非法字元。

    語法層級 (Syntactical)：偵測不符合文法規範的 Token 組合，並透過 gHasUnexpected 進行錯誤標註。

    語義層級 (Semantic)：透過 gDefVar 與 gDefFunc 維護符號表，即時檢測「未定義識別碼 (Undefined Identifier)」。

Symbol Table Management：

    使用 vector 結構儲存定義過的變數 (gDefVar)、型別 (gVarType) 及函式 (gDefFunc)。
    支援作用域管理，區分全域變數與函數內部參數 (gCSDefVar)。

Pretty Printer：

    解析過程中同步建立程式結構，並根據文法邏輯（如 if, while, {}）進行自動縮排與格式化輸出。

## 🛠 技術棧 (Tech Stack)
開發語言：C++

標準庫運用：vector (動態陣列管理), string (Token 處理), stringstream (格式化轉換)

## 📂 程式碼架構分析
Token 處理：透過 IsDigit, IsLetter 與運算子辨識邏輯，實作 Longest Match 策略。

全域狀態控制：利用 gParenthesis (圓括號) 與 gSquareBracket (方括號) 監控語法對稱性。

系統函數支援：內建辨識 ListAllVariables(), ListAllFunctions() 與 Done() 等指令。
     
    The system-supported functions of OurC system are listed below.
    ListAllVariables(); // just the names of the (global) variables,
                        // sorted (from smallest to greatest)
    ListAllFunctions(); // just the names of the (user-defined)
                        // functions, sorted
    ListVariable(char name[]); // the definition of a particular variable
    ListFunction(char name[]); // the definition of a particular function
    Done(); // exit the interpreter
