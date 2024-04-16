clc; clear all; close all;
img = imread('NYC.tif');

prompt1 = 'Enter the values of the fmin: ';
fmin = input(prompt1);
prompt2 = 'Enter the Value of the fmax: ';
fmax = input(prompt2);
prompt3 = 'Enter the Value of the gamma: ';
gamma = input(prompt3);
gmin = 0;
gmax = 255;


%%%% ADOBE PHOTOSHOP "LEVELS" ALGORITHM %%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%

a = (gmax - gmin)^(1 - 1/gamma);

f = double(img);
g = gmin + a*((( f - fmin ) / (fmax - fmin))*(gmax - gmin)).^(1/gamma);


% Clipping the image to be in the range of gmax and gmin

g(g < gmin) = gmin;
g(g > gmax) = gmax;
g = uint8(g);
figure;
montage({img,g});
title('before vs after image')
