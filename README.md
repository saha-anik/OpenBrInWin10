Open Source Biometric Recognition(OpenBr) :A communal biometrics framework supporting the development of open algorithms and reproducible evaluations. It has facial reconition algorithm.

# [OpenBr](http://openbiometrics.org/) Install in Windows 10: 

## Softwares: 

       - Visual Studio Express 2013 for Windows Desktop 
       - CMAKE –3.17.2 /3.0.2(During installation setup select "Add CMake to PATH".)
       - Qt 5.9.9(Last vs13 supported version) 
       - Opencv-2.4.11
       - Openbr

## Envircronment Variables:
       - Create new variable named **OPENCV_DIR** and set value **C:\opencv-2.4.11\build-msvc2013\install\x64\vc12**
       - Add value **C:\openbr\build-msvc2013\install\bin** and **C:\opencv-2.4.11\build-msvc2013\install\x64\vc12\bin** in Path variable.

## Setup OpenCv 2.4.11
       -Consider the free open source program zip extractor if you need a program to unarchive tarballs
       -Move the "opencv-2.4.11" folder to "C:\".
       -Open "VS2013 x64 Cross Tools Command Prompt" (from the Start Menu, select "All Programs" -> "Microsoft Visual Studio 2013" -> "Visual Studio Tools" -> "VS2013 x64 Cross Tools Command Prompt") and enter: 
              cd C:\opencv-2.4.11  
              mkdir build-msvc2013  
              cd build-msvc2013  
              =>If cuda core not present: 
              cmake -G "NMake Makefiles" -DBUILD_PERF_TESTS=OFF -DBUILD_TESTS=OFF -DWITH_FFMPEG=OFF -DCMAKE_BUILD_TYPE=Debug ..  
              =>If cuda core present: 
              cmake -G "NMake Makefiles" -DBUILD_PERF_TESTS=OFF -DBUILD_TESTS=OFF -DWITH_FFMPEG=OFF -DCMAKE_BUILD_TYPE=Debug -DWITH_CUDA:BOOL="0" .. 
              nmake  
              nmake install  
              cmake -DCMAKE_BUILD_TYPE=Release ..  
              nmake  
              nmake install  
              nmake clean 

## Install Qt 5.9.9
      Find qmng.dll (go pro app has) and put it in C:/Qt/5.9.9/msvc2013_64/plugins/imageformats/qmng.dll 

## OpenBr: 
     In command prompt: 
            cd /c  
            git clone https://github.com/biometrics/openbr.git  
            cd openbr  
            git checkout v1.1.0  
            git submodule init  
            git submodule update 
      
      Then Follow this: https://github.com/biometrics/openbr/pull/486/files#diff-c63ce43fc15eb67b7692b8bedfa1e2ac 
            Goto C:\openbr\openbr 
            Open openbr_plugin.cpp 
            Goto line number 1612  
            change independent.set("transform", qVariantFromValue<void*>(transform)) To* this independent.set("transform", QVariant::fromValue(transform)); 
     
      From the VS2013 x64 Cross Tools Command Prompt: 
            cd C:\openbr $ mkdir build-msvc2013  
            cd build-msvc2013  
            cmake -G "CodeBlocks - NMake Makefiles" -DCMAKE_PREFIX_PATH="C:/opencv-2.4.11/build-msvc2013/install;C:/Qt/5.9.9/msvc2013_64" -DCMAKE_INSTALL_PREFIX="./install" -DBR_INSTALL_DEPENDENCIES=ON -DCMAKE_BUILD_TYPE=Release ..  
            nmake  
            nmake install 

 

## Hack OpenBR! 

       From the VS2013 x64 Cross Tools Command Prompt: $ C:\Qt\Tools\QtCreator\bin\qtcreator.exe 
       From the Qt Creator "Tools" menu select "Options..."Under "Kits" select "Desktop (default)" 
       For "Compiler:" select "Microsoft Visual C++ Compiler 12.0 (x86_amd64)" and click "OK" 
       From the Qt Creator "File" menu select "Open File or Project...". 
       Select "C:\openbr\CMakeLists.txt" then "Open". 
       If prompted for the location of CMake, enter "C:\Program Files (x86)\CMake 3.0.2\bin\cmake.exe". 
       Browse to your pre-existing build directory "C:\openbr\build-msvc2013" then select "Next". 
       Select "Run CMake" then "Finish"(Don’t click run button) 
       (Adapt qr to this) 

 

 

 
