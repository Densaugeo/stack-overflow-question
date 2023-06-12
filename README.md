`test.png` is one of the .png files I am trying to crop programmatically. Loading and unloading it with either Python's pillow or Rust's image distorts the colors

`test copy python-pillow.png` is the result of running:
```
from PIL import Image, ImageCms

with Image.open('test.png') as image:
    #image.save('test copy python-pillow.png')
    image.save('test copy python-pillow.png', icc_profile=image.info.get('icc_profile'))
```

`test copy rust-image.png` is the result of running:
```
use image::GenericImageView;

fn main() {
    // Use the open function to load an image from a Path.
    // `open` returns a `DynamicImage` on success.
    let img = image::open("test.png").unwrap();

    // The dimensions method returns the images width and height.
    println!("dimensions {:?}", img.dimensions());

    // The color method returns the image's `ColorType`.
    println!("{:?}", img.color());

    // Write the contents of this image to the Writer in PNG format.
    img.save("test copy rust-image.png").unwrap();
}
```
