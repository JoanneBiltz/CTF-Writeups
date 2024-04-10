# Babel (malware, 403 solves, 50 points)

## Introduction

<p align="left">
  <img height=400 img src=./readme_assets/babel-challenge.PNG/>
</p>

## Solution

The file is c# code very obfuscated.

```
using System;
using System.Collections.Generic;
using System.Text;
using System.IO;
using System.Reflection;
using System.Linq;
namespace RAKSVwqLMTDsnB {
  class pcuMyzvAxeBhINN {
    private static string zcfZIEShfvKnnsZ(string t, string k) {
      string bnugMUJGJayaT = "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ";
      string WgUWdaUGBFwgN = "";
      Dictionary < char, char > OrnBLfjI = new Dictionary < char, char > ();
      for (int i = 0; i < bnugMUJGJayaT.Length; ++i) {
        OrnBLfjI.Add(k[i], bnugMUJGJayaT[i]);
      }
      for (int i = 0; i < t.Length; ++i) {
        if ((t[i] >= 'A' && t[i] <= 'Z') || (t[i] >= 'a' && t[i] <= 'z')) {
          WgUWdaUGBFwgN += OrnBLfjI[t[i]];
        } else {
          WgUWdaUGBFwgN += t[i];
        }
      }
      return WgUWdaUGBFwgN;
    }
    static void Main() {
      string pTIxJTjYJE = "looooong string of giberish here"
	  string YKyumnAOcgLjvK = "lQwSYRxgfBHqNucMsVonkpaTiteDhbXzLPyEWImKAdjZFCOvJGrU";
      Assembly smlpjtpFegEH = Assembly.Load(Convert.FromBase64String(zcfZIEShfvKnnsZ(pTIxJTjYJE, YKyumnAOcgLjvK)));
      MethodInfo nxLTRAWINyst = smlpjtpFegEH.EntryPoint;
      nxLTRAWINyst.Invoke(smlpjtpFegEH.CreateInstance(nxLTRAWINyst.Name), null);
    }
  }
}
	  ```
	  
It took a lot of time to get the code de-obfuscated using copy and paste. This challenge has two parts, de-obfuscate the initial code then de-obfuscate the resulting code.

Here is the code after the first round of de-obfuscating.

```
using System;
using System.Collections.Generic;
using System.Text;
using System.IO;
using System.Reflection;
using System.Linq;
namespace RAKSVwqLMTDsnB {
  class Program {
    private static string Decode(string encodedText, string key) 
    {
      string alphabet = "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ";
      string decodedText = "";
      Dictionary < char, char > charMap = new Dictionary < char, char > ();
      for (int i = 0; i < alphabet.Length; ++i) 
      {
        charMap.Add(key[i], alphabet[i]);
      }
      for (int i = 0; i < encodedText.Length; ++i) 
      {
        if ((encodedText[i] >= 'A' && encodedText[i] <= 'Z') || (encodedText[i] >= 'a' && encodedText[i] <= 'z')) {
          decodedText += charMap[encodedText[i]];
        } else {
          decodedText += encodedText[i];
        }
      }
      return decodedText;
    }
    static void Main() 
    {
      string base64EncodedAssembly = "long string of gibberish here"
	  string decryptionKey = "lQwSYRxgfBHqNucMsVonkpaTiteDhbXzLPyEWImKAdjZFCOvJGrU";

      Console.WriteLine(Decode(base64EncodedAssembly, decryptionKey));
      
    }
  }
}

```
 Initially I was getting `Not so fast!` when running the code. I realized I had to print the decoded assembly to the console then decode in cyberchef. I now have an executable file that windows won't let me run.
 
 <p align="left">
  <img height=300 img src=./readme_assets/babel-result.PNG/>
</p>

I installed Wine on my Kali VM and tried to run the file. The result was more errors.

<p align="left">
  <img height=300 img src=./readme_assets/babel-error.PNG/>
</p>

Used strings on the file and found the flag.

<p align="left">
  <img height=700 img src=./readme_assets/babel-flag.PNG/>
</p>

## Flag

**`flag{b6cfb6656ea0ac92849a06ead582456c}`**

## Tools

- `VS Code`
- `notepad++`
- `strings`
- [CyberChef](https://gchq.github.io/CyberChef/)
- [Wine](https://www.winehq.org/)





