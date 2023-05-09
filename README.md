<#
. 概要
讓鸚鵡在你的殼上跳舞。
. 例子
./鸚鵡舞.ps1
#>

$request  = [ System.Net.HttpWebRequest ]::Create( " http://parrot.live " );
$response  =  $request.GetResponse ( );
$receiveStream  =  $response.GetResponseStream ( );
$readStream  = [ System.IO.StreamReader ]::new( $receiveStream );

[控制台]::TreatControlCAsInput =  $true ;
$initialForegroundColor  = [控制台]::ForegroundColor;
while ( $line  =  $readStream .ReadLine ()) {
  如果（[控制台]::KeyAvailable）{
    $key  = [ System.Console ]::ReadKey( $true )
    if (( $key .modifiers  -band [ ConsoleModifiers ] " control " ) -and ( $key .key  -eq  " C " ))
    {
      打破;
    }
  }

  [控制台]::WriteLine( $line );
}

$ readStream.Close ();
$ receiveStream.Close ();
$request.Abort ( );
[控制台]::TreatControlCAsInput =  $false ;
[控制台]::ForegroundColor =  $initialForegroundColor ;
