Connection
<?php

//Define your host here.
$HostName = "localhost";

//Define your database username here.
$HostUser = "id9817934_test";

//Define your database password here.
$HostPass = "admin123";

//Define your database name here.
$DatabaseName = "id9817934_test";

?>


Insert Data

<?php

include 'DatabaseConfig.php';

// Create connection
$conn = new mysqli($HostName, $HostUser, $HostPass, $DatabaseName);
 
 if($_SERVER['REQUEST_METHOD'] == 'POST')
 {
 $DefaultId = 0;
 
 $ImageData = $_POST['image_path'];
 
 $lname = $_POST['image_name'];
 $fname=$_POST['first_name'];
 $dob=$_POST['dob'];
  $ad=$_POST['ad'];
   $mno=$_POST['mno'];
    $email=$_POST['email'];

 $GetOldIdSQL ="SELECT id FROM UploadImageToServer ORDER BY id ASC";
 
 $Query = mysqli_query($conn,$GetOldIdSQL);
 
 while($row = mysqli_fetch_array($Query)){
 
 $DefaultId = $row['id'];
 }
 
 $ImagePath = "images/$DefaultId.png";
 
 $ServerURL = "https://files.000webhost.com/$ImagePath";
 
 $InsertSQL = "insert into UploadImageToServer (image_path,image_name,first_name,dob,ad,mno,email) values ('$ServerURL','$lname','$fname','$dob','$ad','$mno','$email')";
 
 if(mysqli_query($conn, $InsertSQL)){

 file_put_contents($ImagePath,base64_decode($ImageData));

 echo "Your Image Has Been Uploaded.";
 }
 
 mysqli_close($conn);
 }else{
 echo "Not Uploaded";
 }

?>
