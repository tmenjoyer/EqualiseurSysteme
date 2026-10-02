# Recompiler le programme

## Option A — Depuis Windows avec MinGW-w64 (MSYS2)
```
g++ -std=c++17 -municode -O2 -static -static-libgcc -static-libstdc++ ^
  src/main.cpp -o EqualiseurSysteme.exe ^
  -lole32 -loleaut32 -luuid -lwinmm -lksuser
```

## Option B — Depuis Windows avec Visual Studio (x64 Native Tools Command Prompt)
```
cl /std:c++17 /EHsc /O2 src\main.cpp /link ole32.lib oleaut32.lib winmm.lib ^
  /out:EqualiseurSysteme.exe
```

## Option C — Cross-compilation depuis Linux (ce qui a ete fait ici)
```
sudo apt install mingw-w64 g++-mingw-w64-x86-64
x86_64-w64-mingw32-g++ -std=c++17 -municode -O2 -static -static-libgcc -static-libstdc++ \
  src/main.cpp -o EqualiseurSysteme.exe \
  -lole32 -loleaut32 -luuid -lwinmm -lksuser
```

Aucune dependance externe n'est requise a l'execution (tout est lie
statiquement) : un seul fichier `EqualiseurSysteme.exe`.
