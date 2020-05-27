Captcha
=======

A captcha library that generates audio and image CAPTCHAs.

Updates
-------
Updated library to to generate captchas like this in black and white.
Then NN was trained to solve these captchas. Check it's `GitHub project <https://github.com/avk0/captcha-tensorflow.git>`_.

.. image:: https://user-images.githubusercontent.com/47819971/83060284-e1e04800-a063-11ea-83d7-8ccf387cc7b8.jpg
.. image:: https://user-images.githubusercontent.com/47819971/83060286-e278de80-a063-11ea-8504-afd1fff9a117.jpg



Features
--------

1. Audio CAPTCHAs `DEMO <https://github.com/lepture/captcha/releases/download/v0.1-beta/out.wav>`_
2. Example of target CAPTCHAs. This lib allows to generate such captchas in black and white.

.. image:: https://user-images.githubusercontent.com/47819971/83060288-e3117500-a063-11ea-9a12-5fbde05ec098.jpg

Installation
------------

Install captcha with pip::

    $ git clone https://github.com/avk0/captcha.git
    $ cd captcha
    $ python setup.py install

Usage
-----

Audio and Image CAPTCHAs are in seprated modules:

.. code:: python

    from captcha.audio import AudioCaptcha
    from captcha.image import ImageCaptcha

    audio = AudioCaptcha(voicedir='/path/to/voices')
    image = ImageCaptcha(fonts=['/path/A.ttf', '/path/B.ttf'])

    data = audio.generate('1234')
    audio.write('1234', 'out.wav')

    data = image.generate('1234')
    image.write('1234', 'out.png')

This is the APIs for your daily works. We do have built-in voice data and font
data. But it is suggested that you use your own voice and font data.

Voices
------

We can build our customized voice library with the help of espeak and ffmpeg::

   export ESLANG=en

   mkdir $ESLANG

   for i in {a,b,c,d,e,f,g,h,i,j,k,l,m,n,o,p,q,r,s,t,u,v,w,x,y,z,A,B,C,D,E,F,G,H,I,J,K,L,M,N,O,P,Q,R,S,T,U,V,W,X,Y,Z,0,1,2,3,4,5,6,7,8,9}; do mkdir $ESLANG/$i; espeak -a 150 -s 100 -p 15 -v$ESLANG $i -w $ESLANG/$i/orig_default.wav; ffmpeg -i $ESLANG/$i/orig_default.wav -ar 8000 -ac 1 -acodec pcm_u8 $ESLANG/$i/default.wav; rm $ESLANG/$i/orig_default.wav; done

