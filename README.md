FuelPHP QRCode
==============

QRCode library created as a FuelPHP package.


Usage
=====

Load the QRCode package

<pre lang="php">
// load the package
\Package::load("qrcode");
</pre>

Output the QR directly, used within a view (ugly)

<pre lang="php">
echo \QRCode::png('http://arrggghhh.steadweb.co.uk');
</pre>

or pass the generated QRCode to a view

<pre lang="php"><code>
try
{
        $file   = time() . ".png";
        $qrcode = "";

        // generate the QRCode
        \QRCode::png('http://arrggghhh.steadweb.co.uk', $file, QR_ECLEVEL_L, 6, 4, false);

        // check the file has been generated
        // otherwise throw an exception
        if( ! is_file(DOCROOT . $file))
        {
                throw new Exception("Unable to generate QR code");
        }
        
        $qrcode = Asset::img(Uri::create("/" . $file))
}
catch(\Exception $e)
{
        // log the error
        Log::error($e->getMessage());
        
        // show something, atleast
        $qrcode = "QRCode wasn't generated, derp.";
}

return \View::forge("qrcode", array("qr" => $qrcode), false);
</code></pre>
