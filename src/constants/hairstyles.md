# Hairstyles

The `HairStyle` value encodes both hair color and style in a single numeric ID.

## Encoding Format

```
HairStyle = (HairColor × 100) + Style
HairColor = HairStyle ÷ 100             // integer division
Style = HairStyle % 100                // modulo
```

Examples:
- `537` = Color 3 (Black), Style 30 (New)
- `515` = Color 5 (Red), Style 15 (Nostalgic)
- `625` = Color 6 (Brown), Style 25 (Special)

**Note**: VIP styles (70-90) have a static appearance and the color formula does not affect their visual look.

## Hair Colors

```proto
enum HairColor {
    HAIR_COLOR_BLACK = 3;
    HAIR_COLOR_WHITE = 4;
    HAIR_COLOR_RED = 5;
    HAIR_COLOR_BROWN = 6;
    HAIR_COLOR_GREEN = 7;
    HAIR_COLOR_BLUE = 8;
    HAIR_COLOR_VIOLET = 9;
}
```

## Hair Styles

```proto
enum HairStyle {
    // Nostalgic - 10-16
    HAIR_STYLE_NOSTALGIC_1 = 10;
    HAIR_STYLE_NOSTALGIC_2 = 11;
    HAIR_STYLE_NOSTALGIC_3 = 12;
    HAIR_STYLE_NOSTALGIC_4 = 13;
    HAIR_STYLE_NOSTALGIC_5 = 14;
    HAIR_STYLE_NOSTALGIC_6 = 15;
    HAIR_STYLE_NOSTALGIC_7 = 16;
    
    // Special - 21-25
    HAIR_STYLE_SPECIAL_1 = 21;
    HAIR_STYLE_SPECIAL_2 = 22;
    HAIR_STYLE_SPECIAL_3 = 23;
    HAIR_STYLE_SPECIAL_4 = 24;
    HAIR_STYLE_SPECIAL_5 = 25;
    
    // New - 30-41
    HAIR_STYLE_NEW_1 = 30;
    HAIR_STYLE_NEW_2 = 31;
    HAIR_STYLE_NEW_3 = 32;
    HAIR_STYLE_NEW_4 = 33;
    HAIR_STYLE_NEW_5 = 34;
    HAIR_STYLE_NEW_6 = 35;
    HAIR_STYLE_NEW_7 = 36;
    HAIR_STYLE_NEW_8 = 37;
    HAIR_STYLE_NEW_9 = 38;
    HAIR_STYLE_NEW_10 = 39;
    HAIR_STYLE_NEW_11 = 40;
    HAIR_STYLE_NEW_12 = 41;
    
    // VIP Level 4 - 70-74
    HAIR_STYLE_VIP4_1 = 70;
    HAIR_STYLE_VIP4_2 = 71;
    HAIR_STYLE_VIP4_3 = 72;
    HAIR_STYLE_VIP4_4 = 73;
    HAIR_STYLE_VIP4_5 = 74;
    
    // VIP Level 5 - 75-90
    HAIR_STYLE_VIP5_1 = 75;
    HAIR_STYLE_VIP5_2 = 76;
    HAIR_STYLE_VIP5_3 = 77;
    HAIR_STYLE_VIP5_4 = 78;
    HAIR_STYLE_VIP5_5 = 79;
    HAIR_STYLE_VIP5_6 = 80;
    HAIR_STYLE_VIP5_7 = 81;
    HAIR_STYLE_VIP5_8 = 82;
    HAIR_STYLE_VIP5_9 = 83;
    HAIR_STYLE_VIP5_10 = 84;
    HAIR_STYLE_VIP5_11 = 85;
    HAIR_STYLE_VIP5_12 = 86;
    HAIR_STYLE_VIP5_13 = 87;
    HAIR_STYLE_VIP5_14 = 88;
    HAIR_STYLE_VIP5_15 = 89;
    HAIR_STYLE_VIP5_16 = 90;
}
```

## Client File References

- **`ini/NpcX.ini`**: Contains 145+ `Hair=` entries with values ranging from 0 to 678, used to define NPC hairstyles