The headshot is embedded directly in index.html as a base64 data: URI on the
header <img>, so it renders in print-to-PDF and travels into every roles/*.html copy.
To change the photo: base64-encode the new image and replace the data: URI in index.html.
Hidden when <body> has the no-photo class.
