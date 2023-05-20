# Model H
## Replacement controller board for IBM Model M Keyboard

![Model H controller](https://modelh.club/modelh_assembled.jpg)

The [IBM Enhanced Keyboard (Model
M)](https://en.wikipedia.org/wiki/Model_M_keyboard) is widely
considered the best keyboard for its typing experience. First produced
in 1985, it was made of high quality materials and is very
durable. IBM produced over 10 millions units, and because of their
durability, there are still many working keyboards today.

![IBM Enhanced Keyboard](https://upload.wikimedia.org/wikipedia/commons/4/48/IBM_Model_M.png)

However, those keyboards were designed for the [PS/2
port](https://en.wikipedia.org/wiki/PS/2_port), which is rarely seen
in recent computers. Some units that were shipped with terminals even
used a RJ-45 interface. As a result, it can be difficult to use this
keyboard with modern computers.

If you want to enjoy the great typing experience of an IBM Model M on a modern computer, you have basically 3 options:

1. You can buy a new unit with a USB interface at [Unicomp](https://www.pckeyboard.com/page/product/NEW_M).
2. You can use an active [PS/2 to USB converter](https://www.clickykeyboards.com/product/ps-2-to-usb-adapter-converter-for-keyboards/). That solution will not work for RJ-45 Model Ms, though.
3. You can replace the original controller with a new one supporting USB. That is what this project proposes.

Out of those 3 options, creating your own controller is clearly the
most involved. That being said, the result is very neat. You'll end up
with a native USB connector that is very well integrated with the
keyboard.

![USB port](https://modelh.club/modelh_usb_back.jpg)

In addition, the controller firmware uses
[QMK](https://github.com/qmk/qmk_firmware), which will allow you to
remap your keys. This is very handy to add media keys and other custom
combinations you may need.

To make your own board, you don't need any knowledge in electronics, however, you'll have to do a bit of soldering.

## Related work

This work is not the first attempt at a replacement controller for the Model M. Here are a few related projects:

- https://www.schwingen.org/modelm-usb/
- https://github.com/ashpil/Model-M-Type-C
- https://github.com/sje-mse/yacobo
- https://store.level1techs.com/products/mstar-classic-model-m-controller-conversion-kit

## Production tutorial

In this tutorial, we will go into all the steps needed to make your Model H controller board.

### PCB
Here, we show how to produce the PCB with
[JLCPCB](jlcpcb.com). There are many similar providers. Feel free to
choose a different one. Note that the bill of material has been
optimized for parts available at JLCPCB. Should you choose a different
provider, you might have to replace some parts.

1. Go to [JLCPCB](jlcpcb.com) and create an account.
2. On the JLCPCB home page, use the button `Add gerber file` to upload the file `gerber.zip` found in the `production` folder of this repo. You should see a page like the image below. Leave the default options.

![](pictures/jlcpcb1.png)

3. At the bottom of the page, select `PCB Assembly`. Leave the default options, but you may want to change the `PCBA Qty` to 2. Also, select `Yes` for `Confirm Parts Placement`.

![](pictures/jlcpcb2.png)

4. On the right of the page, click on `NEXT`.
5. You can now visualize both sides of your PCB. Then click on `NEXT` and upload the two files `bom.csv` and `positions.csv` from the `production` folder.
6. Click on `Process BOM & CPL`. At this point, you should see a list of all the components for your design. If all of them are available, click `NEXT`. If a part is out of stock, click on the magnifying glass to select a replacement. Alternatively, you can wait until the part is in stock again. All components of the design were chosen among JLCPCB's __basic parts__ and should normally be available.

![](pictures/jlcpcb3.png)

7. This page should show you the parts placement (as shown below). Select the 3D view and verify that the components are placed properly. Then click `NEXT`.

![](pictures/jlcpcb4.png)

8. Select Product Description: Office Appliance.../Keyboard...

9. Save to Cart, Check Out.

#### Cost
At the time of writing (May 2023), the cost of 5 PCBs with 2 assembled was $21 (without shipping).

---

### 3D Printed connector spacer
To maintain the USB connector and the controller board in place, you will have to 3D print a small connector spacer to be inserted around the USB connector.
The file to be printed is located at `shim/shim.stl`.
You can use any 3D printing service for this, however it might be a good idea to use JLCPCB and group the order with the PCB one.

---

### Additional Components

While you wait for your PCB to be fabricated, you can order the few
additional components that you'll need to hand solder onto the
board. But first, you need to disassemble your keyboard and check what
kind of wiring you have. Look at this [tutorial](https://blog.nathanv.me/posts/ibm-model-m-cleaning/) for this.

There are several types of connectors for the LEDs.

1. If you don't have LEDs, that's easy. You'll just need a 16-position and a 8-position FFC connectors.
2. If you have an old keyboard with the type of LED cable shown below, you'll have to figure out the type of connector you'll need for it. In addition, you'll need a 16-position and 8-position FFC connectors.
![LED wire](https://github.com/mschwingen/hardware/raw/master/modelm-usb/images/LEDs_Wire_s.jpg)

3. If your LEDs are connected with a FFC cable like the one shown below, you'll need a 16-position, 8-position and 4-position FFC connectors.
![LED FFC](site/16_8_4.jpg)

4. Finally, if you LEDs are integrated to the membrane rows connector (see below), you'll need a 16-position and a 12-position FFC connectors.
![LED integrated](site/16_12.jpg)

Below is the list of components you will need to order:

| Part                      | Link                                                                                           | Quantity |
|---------------------------|------------------------------------------------------------------------------------------------|----------|
| 16-POS FFC TE connector   | https://www.digikey.com/en/products/detail/te-connectivity-amp-connectors/6-520315-6/688643    | 1        |
| 8-POS FFC TE connector    | https://www.digikey.com/en/products/detail/te-connectivity-amp-connectors/5-520315-8/688639    | 0/1      |
| 4-POS FFC TE connector    | https://www.digikey.com/en/products/detail/te-connectivity-amp-connectors/5-520315-4/2262309   | 0/1      |
| 12-POS FFC TE connector   | https://www.digikey.com/en/products/detail/te-connectivity-amp-connectors/6-520315-2/1137020   | 0/1      |
| USB-B connector           | https://www.digikey.com/en/products/detail/te-connectivity-amp-connectors/292304-1/773785      | 1        |
| Debug port connector      | https://www.digikey.com/en/products/detail/on-shore-technology-inc/302-S101/2178422            | 1        |
| 6-POS header connector    | https://www.digikey.com/en/products/detail/w%C3%BCrth-elektronik/61300621121/4846835           | 1        |
| jumper                    | https://www.digikey.com/en/products/detail/w%C3%BCrth-elektronik/60900213421/2508447           | 2        |
| USB A-B cable             | https://www.digikey.com/en/products/detail/tripp-lite/U022-006-BE/7104962                      | 1        |

---

### Soldering

Once you received the controller board and all the components, it's
time to solder them to the board. If you use the right technique,
soldering is not that hard. This
[tutorial](https://learn.sparkfun.com/tutorials/how-to-solder-through-hole-soldering/all)
goes in a lot of details and the video explains very well how to
easily solder your through-hole components into the board. If you've
never soldered before, I would recommend practicing on a different
board before assembling your Model H.

You can clearly see where to place the components on the board picture
at the top of this page. Pay attention to the FFC connectors
direction. Note the white lines on the board indicating the right
connectors direction.

### Bootloader

At this point, you should have a complete controller. However, do not
insert it into your keyboard just yet. You still need to program your
controller and it is much easier to do it when not attached to the
keyboard.

The STM32F103 micro-controller from the board does not ship with a USB
bootloader. This means that you cannot use the USB port just yet. If
you plug the controller to your computer, you should see the
right-most LED light up, but the computer will not recognize the
controller.

Since we cannot use the USB port to communicate with the controller,
we will have to rely on the `debug` port. To connect it to your
computer, you will need to a ST-Link device, such as the one shown
below. Those devices can be found on [Amazon](https://www.amazon.com/dp/B07SQV6VLZ?psc=1&ref=ppx_yo2ov_dt_b_product_details) for ~$10.

![ST-Link](https://github.com/jberclaz/stm32f103-keyboard-bootloader/blob/master/img/stlink.jpg)
