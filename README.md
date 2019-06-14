Documentation: https://pdollar.github.io/toolbox/

# Modified toolbox to run under Octave
This modification is tested under debian just to run [pdollar_edges_octave](github.com/ardiya/pdollar_edges_octave)'s `edgesEvalDir`! I haven't create all mex for Octave, but it should be easy to compile other mex files with instruction below

**Features**
- Added `parcellfun` option in fEvalDir as Octave's alternative to Matlab's `parfor`

## Installing Octave 4.4.1
I'ts the latest Octave4. Octave 4.0.0 from debian is causing segfault!! Octave 5.1.0's parallel package doesn't compile
Download from https://ftpmirror.gnu.org/octave
```
sudo apt purge octave # Remove existing Octave from apt
sudo apt build-dep octave # Install octave prerequisites
./configure
make -j8
sudo make install
octave --eval "pkg install -forge image parallel struct"
```

## Compile cpp to mex
These are examples of files in `channels/private` folder, I believe you would be able to easily add other folders.
```
cd channels/private
for item in convConst.cpp gradientMex.cpp imPadMex.cpp imResampleMex.cpp rgbConvertMex.cpp;
    do mkoctfile --mex -DMATLAB_MEX_FILE $item;
done
cd ../..
```

## Install (Add path to octave)
Run following commands in `octave`
```octave
addpath(genpath(pwd))
savepath
```
