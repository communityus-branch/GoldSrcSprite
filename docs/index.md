# GoldSrcSprite
GoldsrcSprite is a simple .NET Standard library to handle GoldSrc engine sprite (.spr) files.

## Usage Examples
```csharp
// Load sprite
var sprite = GoldSrcSprite.FromFile("sprite.spr");

// Get bitmap of the first frame
using(var bmp = sprite.Frames[0].GetBitmap()) {
	// Save as bmp
    bmp.Save("sprite.bmp");
}

// Save sprite
sprite.SaveToFile("sprite.spr");
```

## About .spr files
The format itself is flexible, however keep in mind that game engines might not load the most extreme cases.
* A sprite can only use 256 colors with it's own palette
* Can specify how the sprite should be oriented and rendered
* Each sprite can contain multiple frames
* Each frame share the same palette
* Each frame can be different sizes and have a different center origin point

## More Examples

### Example #1: Creating a sprite from scratch
The following example will create a "sprite.spr" file with this sprite: ![Image of Example 1 sprite](https://jpiolho.github.io/GoldSrcSprite//images/example1.png)
```csharp
GoldSrcSprite sprite = new GoldSrcSprite();

// Set some basic settings
sprite.Type = GoldSrcSpriteType.ParallelUpright;
sprite.TextureFormat = GoldSrcSpriteTextureFormat.Normal;
sprite.Synchronization = GoldSrcSpriteSynchronization.Synchronized;

// Create the palette
sprite.Palette = new Color[256];
sprite.Palette[0] = Color.Red;
sprite.Palette[1] = Color.Green;
sprite.Palette[2] = Color.Blue;
sprite.Palette[3] = Color.White;

// Create the frame
var frame = new GoldSrcSpriteFrame(sprite,2,2);

// Frame basic settings
frame.OriginX = 1;
frame.OriginY = 1;

// Actual image data
new byte[]
{
0,1,
2,3
}.CopyTo(frame.Data, 0);

// Add the frame to the sprite
sprite.Frames.Add(frame);

// Save the sprite
sprite.SaveToFile("sprite.spr");
```

