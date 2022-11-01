AHTBITW.github.io
Hello World
<HTML>
<HEAD>

<SCRIPT language=JavaScript>

arrCos = new Array(360);    /* Hold the COS lookup table for 0 to 359 deg */
arrSin = new Array(360);    /* Hold the SIN lookup table for 0 to 359 deg */

for (i=0;i<360;i++) {
    arrSin[i] = Math.sin(i * Math.PI / 180);
    arrCos[i] = Math.cos(i * Math.PI / 180);
}

function rotate(objID, x, y, r, deg, rinc) {
    /* objID    - the ID of the object we're gonna manipulate
     * x        - current object x-axis
     * y        - current object y-axis
     * r        - current object radius
     * deg      - current rotation around axis in degrees
     * rinc     - by how much we'll increment the radius this time
     */

    y = r * arrSin[deg];
    x = r * arrCos[deg];
    
    document.all[objID].style.pixelLeft = x;
    document.all[objID].style.pixelTop = y+r+10;
    
    if (deg % 60 == 0) r += rinc;
    
    /* Has the radius reached it's maximum/minumum? If so, change the sign of the rinc
     * so that instead of incrementing we decrement - and visa versa
     */
    if (r > 60 || r < 10) {
        rinc *= -1;
        r += rinc;
    }
    
    deg += 5;
    if (deg >= 360) deg = 0;

    setTimeout("rotate('" + objID + "'," + x + "," + y + "," + r + "," + deg + "," + rinc + ")", 10);
}

function highlight(objNum, lastNum) {
    /* objNum   -   which object to highlight
     * lastNum  -   which object is currently highlighted
     */
     
    document.all["obj" + objNum].style.color = "#FFFFFF";
    document.all["obj" + objNum].style.fontStyle = "italic";
    
    if (lastNum != 0) document.all["obj" + lastNum].style.color = "";
    if (lastNum != 0) document.all["obj" + lastNum].style.fontStyle = "";
    
    lastNum = objNum;
    if (++objNum > 3) objNum = 1;   /* Have we reached the last object? */

    document.all["obj" + objNum].style.color = "#AAAAAA";
    
    setTimeout("highlight(" + objNum+ "," + lastNum + ")", 2000);
}

function doit() {
    x=0;            /* initial x-axis position  */
    y=0;            /* initial y-axis position  */
    r=10;           /* initial radius           */
    deg=0;          /* initial rotation around axis (in degrees) */
    rinc = 1;       /* radius increment         */

    /* Begin rotating each phrase with possible offsets to the initial values */
    rotate("obj1", x, y, r+10, deg, rinc);
    rotate("obj2", x, y, r, deg+45, rinc);
    rotate("obj3", x, y, r+20, deg+90, rinc);
    rotate("obj4", x, y, r, deg+270, rinc);
    
    /* Begin highlighting each phase in turn */
    highlight(1,0);
}

</SCRIPT>

<STYLE>.rotateOBJ {
 POSITION: relative
}
</STYLE>

</HEAD>
<BODY bgColor=black link=red onload=doit() text=white vLink=red>
<P>
<CENTER><FONT color=#cccccc><B><I><FONT face="" size=5><SPAN class=rotateOBJ 
id=obj1>"Никогда не</SPAN></FONT><BR><FONT face="" size=5><SPAN 
class=rotateOBJ id=obj2>знаешь чем</SPAN></FONT><BR><FONT face="" 
size=5><SPAN class=rotateOBJ id=obj3>все это"</SPAN></FONT><BR></I><FONT 
face="" size=3><SPAN class=rotateOBJ id=obj4>закончится</SPAN></FONT> 
</CENTER></B></FONT>
<!-- copyright (i7) --><div align="center"><a href="http://www.ucoz.ru/" title="Создать сайт бесплатно"><img style="margin:0;padding:0;border:0;" alt="Hosted by uCoz" src="http://s203.ucoz.net/img/cp/11.gif" width="80" height="15" title="Hosted by uCoz" /></a><br /></div><!-- /copyright -->
</body></html>
