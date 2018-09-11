# Email Development
A collection of useful tips and tricks related to Email Development.

### Boilerplate
Use the below snippet for a new email doc.
```
<!DOCTYPE html>
<html lang="en">
<head>
  <meta http-equiv="content-type" content="text/html;" charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge" />
  <title></title>
  <style>
    /* CLIENT-SPECIFIC STYLES */
    body, table, td, a { -webkit-text-size-adjust: 100%; -ms-text-size-adjust: 100%; }
    table, td { mso-table-lspace: 0pt; mso-table-rspace: 0pt; }
    img { -ms-interpolation-mode: bicubic; }

    /* RESET STYLES */
    img { border: 0; height: auto; line-height: 100%; outline: none; text-decoration: none; }
    table { border-collapse: collapse !important; }
    body { height: 100% !important; margin: 0 !important; padding: 0 !important; width: 100% !important; }
  </style>
</head>
<body style="margin: 0 !important; padding: 0 !important;">

</body>
</html>
```

### Preview Text
Use the following snippet to add some preview text that will appear in the email client. The first div contains the preview text and some styles to hide the text so it doesn't appear in the actual email. The second div includes a bunch of non-breaking spaces characters to push the rest of the email content down the page when viewed within the inbox. These spaces do not appear in the actual email.
```
<div style="display: none; max-height: 0px; overflow:hidden; mso-hide:all;">
  preheader text goes here....displays in client below subject but not in email itself
</div>
<div style="display: none; max-height: 0px; overflow:hidden; mso-hide:all;">
  &nbsp;&zwnj;&nbsp;&zwnj;&nbsp;&zwnj;&nbsp;&zwnj;&nbsp;&zwnj;&nbsp;&zwnj;&nbsp;&zwnj;&nbsp;&zwnj;&nbsp;&zwnj;&nbsp;&zwnj;&nbsp;&zwnj;&nbsp;&zwnj;&nbsp;&zwnj;&nbsp;&zwnj;&nbsp;&zwnj;&nbsp;&zwnj;&nbsp;&zwnj;&nbsp;&zwnj;&nbsp;&zwnj;&nbsp;&zwnj;&nbsp;&zwnj;&nbsp;&zwnj;&nbsp;&zwnj;&nbsp;&zwnj;&nbsp;&zwnj;&nbsp;&zwnj;&nbsp;&zwnj;&nbsp;&zwnj;&nbsp;&zwnj;&nbsp;&zwnj;&nbsp;&zwnj;&nbsp;&zwnj;&nbsp;&zwnj;&nbsp;&zwnj;&nbsp;&zwnj;&nbsp;&zwnj;&nbsp;&zwnj;&nbsp;&zwnj;&nbsp;&zwnj;&nbsp;&zwnj;&nbsp;&zwnj;&nbsp;&zwnj;&nbsp;&zwnj;&nbsp;&zwnj;&nbsp;&zwnj;&nbsp;&zwnj;&nbsp;&zwnj;&nbsp;&zwnj;&nbsp;&zwnj;&nbsp;&zwnj;&nbsp;&zwnj;&nbsp;&zwnj;&nbsp;&zwnj;&nbsp;&zwnj;&nbsp;&zwnj;&nbsp;&zwnj;&nbsp;&zwnj;&nbsp;&zwnj;&nbsp;&zwnj;&nbsp;&zwnj;&nbsp;&zwnj;&nbsp;&zwnj;&nbsp;&zwnj;&nbsp;&zwnj;&nbsp;&zwnj;&nbsp;&zwnj;&nbsp;&zwnj;&nbsp;&zwnj;&nbsp;&zwnj;&nbsp;&zwnj;&nbsp;&zwnj;&nbsp;&zwnj;&nbsp;&zwnj;&nbsp;&zwnj;&nbsp;&zwnj;&nbsp;&zwnj;&nbsp;&zwnj;&nbsp;&zwnj;&nbsp;&zwnj;&nbsp;&zwnj;&nbsp;&zwnj;&nbsp;&zwnj;&nbsp;&zwnj;&nbsp;&zwnj;
</div>
```

### Tables & Outlook
Emails are primarily coded using table tags and nested tables to achieve the various multi-column layouts that are popular in email campaigns. In stead of coding for browsers, you end up coding for email clients when developing emails. Outlook in particular has some weird quirks when performing math on table widths. Generally if you want a 2 column layout to span equally across the page, you need to set their widths so the add up to just under 100%. Outlook tends to add extra space and will cause your columns to stack.

### Using Web Fonts
Web fonts can be added to the email in the usual ways. However, some clients do not support them so you need to be good about providing fallbacks. Outlook can sometimes have issues falling back to one of your listed fallback fonts. A fix for this is to wrap your @font-face declaration in a simple media query. See the following example.
```
@media{
  @font-face {
  font-family: 'Roboto';
  font-style: normal;
  font-weight: 400;
  src: local('Roboto'), local('Roboto-Regular'), url(https://fonts.gstatic.com/s/roboto/v18/KFOmCnqEu92Fr1Mu72xKOzY.woff2) format('woff2');
  unicode-range: U+0460-052F, U+1C80-1C88, U+20B4, U+2DE0-2DFF, U+A640-A69F, U+FE2E-FE2F;
  }
}
```

### Link Reset Styles
Some email clients can end up overriding link styles and display their own styles. Use the reset styles below to account for this is GMail and Apple Mail. Note that for the GMail resets, you need to add and id of "body" to the body tag.
```
/* iOS Blue Links */
a[x-apple-data-detectors] {
  color: inherit !important;
  text-decoration: none !important;
  font-size: inherit !important;
  font-family: inherit !important;
  font-weight: inherit !important;
  line-height: inherit !important;
}

/* Gmail Blue Links (need to add id of body to the body tag)*/
u + #body a {
  color: inherit;
  text-decoration: none;
  font-size: inherit;
  font-family: inherit;
  font-weight: inherit;
  line-height: inherit;
}
```

### Buttons
There a couple tricks for making buttons. The first snippet below uses the padding within the table cell to create space. The problem is that only the text is clickable. The second snippet creates a thick border around the link element to create the button. Using this method the entire button becomes clickable.
```
<!-- PADDING-BASED BUTTON -->
<table border="0" cellspacing="0" cellpadding="0">
  <tr>
    <td bgcolor="#357edd" style="padding: 20px 40px 18px 40px; -webkit-border-radius: 8px;" align="center">
      <a href="https://google.com" target="_blank" style="font-size: 18px; font-family: sans-serif; color: #ffffff; text-decoration: none; display: block;">Google &rarr</a>
    </td>
  </tr>
</table>


<!-- BORDER-BASED BUTTON -->
<table border="0" cellspacing="0" cellpadding="0">
  <tr>
    <td>
      <a href="https://google.com" target="_blank" style="font-size: 18px; font-family: sans-serif; color: #ffffff; text-decoration: none; border-radius: 8px; -webkit-border-radius: 8px; background-color: #357edd; border-top: 20px solid #357edd; border-bottom: 18px solid #357edd; border-right: 40px solid #357edd; border-left: 40px solid #357edd; display: inline-block;">Google &rarr</a>
    </td>
  </tr>
</table>
```
#### Bulletproof Buttons
**https://buttons.cm/** - A resource for generating buttons based on CSS selections. The generated button is built using the VML language and works across most clients, but not all.

**http://htmlarrows.com** - A library HTML symbols and ASCII codes to use with button / link creation.


### Images
There are really 3 file types you need to worry about: JPG, PNG, and GIF. JPGs are good for photographs and images with complex color schemes. They can develop artifacts when compressed beyond a reasonable limit. PNG is good for logos, simple color schemes and images requiring transparency. GIF is similar to PNG but is used for animation. Sizes for PNG and GIF can really balloon in size. For emails, it's important to keep the file sizes to a minimum. Use the following default snippet for adding an image.
```
<!-- IMAGE MODULE -->
<tr>
  <td align="center" style="padding: 60px 10px 40px 10px;">
    <a href="#">
      <img src="NEED ABSOLUTE PATH" alt="alt text here" width="600" border="0" style="display: block background-color: #000000; color: #ffffff; font-family: sans-serif; font-size: 32px; font-weight: bold; width: 100%; max-width: 100%; min-width: 200px">
    </a>
  </td>
</tr>
```
Some notes on the above snippet. **Display is set to block** to remove white space between images for outlook clients. Setting **border to 0** ensures a border does not get added when using the image as a link. Lots of styles are included for **alt text** since many people disable email images. Width attributes are for responsive images. You may also use a background image using either CSS or the **background directive** (which is deprecated but still used in a lot of older clients). When using background images, be sure to specify a fallback color to prevent text readability issues.
