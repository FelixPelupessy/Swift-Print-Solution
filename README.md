# Swift-Print-Solution
Aplikasi Print Jarak Jauh 
Kelompok 6 Cendrawasih Software Innovation
<!DOCTYPE html>
<html lang="en">

<head>
    <?php include "link.php"; ?>
</head>

<?php
// Jika form disubmit
if (isset($_POST['hapus_dokumen'])) {
    // Ambil data dari form
    $id_dokumen = $_POST['id_dokumen'];

    // Query untuk menyimpan data ke database
    $query = "DELETE FROM dokumen WHERE id_dokumen = '$id_dokumen'";

    if (mysqli_query($conn, $query)) {
        $script = "
                <script>
                    Swal.fire({
                        icon: 'success',
                        title: 'Dokumen berhasil dihapus!',
                        timer: 3000,
                        timerProgressBar: true,
                        showConfirmButton: false
                    });
                </script>
            ";
    } else {
        $script = "
                <script>
                    Swal.fire({
                        icon: 'error',
                        title: 'Dokumen Gagal Dihapus!',
                        timer: 3000,
                        timerProgressBar: true,
                        showConfirmButton: false
                    });
                </script>
            ";
    }
}



?>


<body id="page-top">

    <!-- Page Wrapper -->
    <div id="wrapper">

        <!-- Sidebar -->
        <?php include "sidebar.php"; ?>
        <!-- End of Sidebar -->

        <!-- Content Wrapper -->
        <div id="content-wrapper" class="d-flex flex-column">

            <!-- Main Content -->
            <div id="content">

                <!-- Topbar -->
                <?php include "topbar.php"; ?>
                <!-- End of Topbar -->

                <!-- Begin Page Content -->
                <div class="container-fluid">
                    <!-- DataTales Example -->
                    <div class="card shadow mb-4">
                        <div class="card-header py-3">
                            <h6 class="m-0 font-weight-bold text-primary">Daftar Dokumen</h6>
                        </div>
                        <div class="card-body">
                            <div class="table-responsive">
                                <table class="table table-bordered" id="dataX" width="100%" cellspacing="0">
                                    <thead>
                                        <tr>
                                            <th>No</th>
                                            <th>Nama</th>
                                            <th>Alamat</th>
                                            <th>No Telp</th>
                                            <th>Email</th>
                                            <th>Metode Pengambilan</th>
                                            <th>File</th>
                                            <th>Tanggal Pengambilan</th>
                                            <th>Aksi</th>
                                        </tr>
                                    </thead>
                                    <tbody>
                                        <?php
                                        $dokumen = mysqli_query($conn, "SELECT * FROM dokumen");
                                        $i = 1;
                                        ?>
                                        <?php foreach ($dokumen as $td) : ?>
                                        <tr>
                                            <td><?= $i;
                                                    $i++; ?></td>
                                            <td><?= $td['nama_lengkap'] ?></td>
                                            <td><?= $td['alamat'] ?></td>
                                            <td><?= $td['notelp'] ?></td>
                                            <td><?= $td['email'] ?></td>
                                            <td><?= $td['metode_pengambilan'] ?></td>
                                            <td><a href="../dokumen/<?= $td['nama_file']; ?>" download="">Unduh File</a>
                                            </td>
                                            <td>
                                                <?= date('d F, Y', strtotime($td['tanggal_pengambilan'])); ?>
                                            </td>
                                            <td>
                                                <div class="d-flex">
                                                    <?php 
                                                            $notelp = $td['notelp'];
                                                            $nama_lengkap = $td['nama_lengkap'];
                                                        ?>
                                                    <a href="https://web.whatsapp.com/send?phone=<?= $notelp; ?>&text=Halo,%20<?= $nama_lengkap; ?>"
                                                        target="_blank" class="btn btn-info">Konfirmasi</a>
                                                    <form action="" method="POST">
                                                        <input type="hidden" name="id_dokumen"
                                                            value="<?= $td['id_dokumen']; ?>">
                                                        <button type="submit" name="hapus_dokumen"
                                                            class="btn btn-danger">Hapus</button>
                                                    </form>
                                                </div>
                                            </td>
                                        </tr>
                                        <?php endforeach; ?>
                                    </tbody>
                                </table>
                            </div>
                        </div>
                    </div>
                </div>

            </div>
            <!-- End of Main Content -->

            <!-- Footer -->
            <?php include "footer.php"; ?>
            <!-- End of Footer -->

        </div>
        <!-- End of Content Wrapper -->

    </div>
    <!-- End of Page Wrapper -->

    <!-- Scroll to Top Button-->
    <a class="scroll-to-top rounded" href="#page-top">
        <i class="fas fa-angle-up"></i>
    </a>

    <?php include "plugin.php"; ?>
    <?php
    if (isset($script)) {
        echo $script;
    }
    ?>

    <script>
    $(document).ready(function() {
        $('#dataX').DataTable({
            "language": {
                "url": "//cdn.datatables.net/plug-ins/9dcbecd42ad/i18n/Indonesian.json",
                "oPaginate": {
                    "sFirst": "Pertama",
                    "sLast": "Terakhir",
                    "sNext": "Selanjutnya",
                    "sPrevious": "Sebelumnya"
                },
                "sInfo": "Menampilkan _START_ sampai _END_ dari _TOTAL_ data",
                "sSearch": "Cari:",
                "sEmptyTable": "Tidak ada data yang tersedia dalam tabel",
                "sLengthMenu": "Tampilkan _MENU_ data",
                "sZeroRecords": "Tidak ada data yang cocok dengan pencarian Anda"
            }
        });
    });
    </script>
</body>

</html>
Footer

<footer class="sticky-footer bg-white" style="position: fixed; bottom:0; width:100%">
    <div class="container my-auto">
        <div class="copyright text-center my-auto">
            <span>Copyright &copy; SWITFT PRINT <?= date('Y'); ?></span>
        </div>
    </div>
</footer>

Link
<meta charset="utf-8">
<meta http-equiv="X-UA-Compatible" content="IE=edge">
<meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
<meta name="description" content="">
<meta name="author" content="">
<title>Swift Print</title>
<link rel="icon" href="../img/logo.png" type="image/x-icon">
<link href="../vendor/fontawesome-free/css/all.min.css" rel="stylesheet" type="text/css">
<link href="../css/sb-admin-2.min.css" rel="stylesheet">
<link href="../vendor/datatables/dataTables.bootstrap4.min.css" rel="stylesheet">
<link rel="stylesheet" href="../vendor/fontawesome-free/css/fontawesome.css">
<script src="../vendor/jquery/jquery.min.js"></script>
<link rel="stylesheet" href="../vendor/sweetalert2/dist/sweetalert2.min.css">
<?php

session_start();
include '../functions.php';
$id_user = $_SESSION['id_user'];

if (!isset($_SESSION["admin"])) {
    header("Location: ../login.php");
    exit;
}

?>


Plugin
<!-- Logout Modal-->
<div class="modal fade" id="logoutModal" tabindex="-1" role="dialog" aria-labelledby="exampleModalLabel" aria-hidden="true">
    <div class="modal-dialog" role="document">
        <div class="modal-content">
            <div class="modal-header">
                <h5 class="modal-title" id="exampleModalLabel">Yakin Ingin Logout?</h5>
                <button class="close" type="button" data-dismiss="modal" aria-label="Close">
                    <span aria-hidden="true">×</span>
                </button>
            </div>
            <div class="modal-body">Setelah <b>Logout</b>, untuk masuk ke sistem ini anda diharuskan <b>Login</b> terlebih.</div>
            <div class="modal-footer">
                <button class="btn btn-secondary" type="button" data-dismiss="modal">Cancel</button>
                <a class="btn btn-primary" href="../logout.php">Logout</a>
            </div>
        </div>
    </div>
</div>


<script src="../vendor/jquery/jquery.min.js"></script>
<script src="../vendor/bootstrap/js/bootstrap.bundle.min.js"></script>
<script src="../vendor/jquery-easing/jquery.easing.min.js"></script>
<script src="../js/sb-admin-2.min.js"></script>
<script src="../vendor/datatables/jquery.dataTables.min.js"></script>
<script src="../vendor/datatables/dataTables.bootstrap4.min.js"></script>
<script src="../vendor/chart.js/Chart.min.js"></script>
<script src="../js/demo/chart-area-demo.js"></script>
<script src="../js/demo/chart-pie-demo.js"></script>
<script src="../js/demo/datatables-demo.js"></script>
<script src="../vendor/sweetalert2/dist/sweetalert2.min.js"></script>

Sidebar
<ul class="navbar-nav bg-gradient-primary sidebar sidebar-dark accordion" id="accordionSidebar">

    <!-- Sidebar - Brand -->
    <a class="sidebar-brand d-flex align-items-center justify-content-center" href="index.php">
        <small>
            SWIFT PRINT <br>
            <i>Admin</i>
        </small>
    </a>

    <!-- Divider -->
    <hr class="sidebar-divider my-0">

    <!-- Nav Item - Dashboard -->
    <li class="nav-item active">
        <a class="nav-link" href="index.php">
            <i class="fas fa-fw fa-home"></i>
            <span>Daftar Dokumen</span></a>
    </li>

    <!-- Divider -->
    <hr class="sidebar-divider">

    <!-- Sidebar Toggler (Sidebar) -->
    <div class="text-center d-none d-md-inline">
        <button class="rounded-circle border-0" id="sidebarToggle"></button>
    </div>


</ul>

Topbar
<nav class="navbar navbar-expand navbar-light bg-white topbar mb-4 static-top shadow">

    <!-- Sidebar Toggle (Topbar) -->
    <button id="sidebarToggleTop" class="btn btn-link d-md-none rounded-circle mr-3">
        <i class="fa fa-bars"></i>
    </button>

    <!-- Topbar Navbar -->
    <ul class="navbar-nav ml-auto">

        <!-- Nav Item - User Information -->
        <li class="nav-item dropdown no-arrow">
            <a class="nav-link dropdown-toggle" href="#" id="userDropdown" role="button" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
                <span class="mr-2 d-none d-lg-inline text-gray-600 small">Halo <?= $_SESSION['username']; ?> ! </span>
            </a>
            <!-- Dropdown - User Information -->
            <div class="dropdown-menu dropdown-menu-right shadow animated--grow-in" aria-labelledby="userDropdown">
                <a class="dropdown-item" href="../logout.php">
                    <i class="fas fa-sign-out-alt fa-sm fa-fw mr-2 text-gray-400"></i>
                    Logout
                </a>
            </div>
        </li>

    </ul>

</nav>

9.2	User 

Index 
<!DOCTYPE html>
<html lang="en">

<head>
    <?php include "link.php"; ?>
</head>

<body id="page-top">

    <!-- Page Wrapper -->
    <div id="wrapper">

        <!-- Sidebar -->
        <?php include "sidebar.php"; ?>
        <!-- End of Sidebar -->

        <!-- Content Wrapper -->
        <div id="content-wrapper" class="d-flex flex-column">

            <!-- Main Content -->
            <div id="content">

                <!-- Topbar -->
                <?php include "topbar.php"; ?>
                <!-- End of Topbar -->

                <!-- Begin Page Content -->
                <div class="container-fluid">

                    <!-- Page Heading -->
                    <div class="container w-100 mx-0">
                        <div class="card shadow mb-4">
                            <div class="card-header py-3">
                                <h2 class="my-2 font-weight-bold text-primary">
                                    Dashboard
                                </h2>
                            </div>

                        </div>

                        <!-- Content Row -->

                    </div>
                    <!-- /.container-fluid -->

                </div>
                <!-- End of Main Content -->

                <!-- Footer -->
                <?php include "footer.php"; ?>
                <!-- End of Footer -->

            </div>
            <!-- End of Content Wrapper -->

        </div>
        <!-- End of Page Wrapper -->

        <!-- Scroll to Top Button-->
        <a class="scroll-to-top rounded" href="#page-top">
            <i class="fas fa-angle-up"></i>
        </a>

        <?php include "plugin.php"; ?>
</body>

</html>

Dokumen Terkirim
<!DOCTYPE html>
<html lang="en">

<head>
    <?php include "link.php"; ?>
</head>

<?php
// Jika form disubmit
if (isset($_POST['kirim'])) {
    // Ambil data dari form
    $nama_lengkap = $_POST['nama_lengkap'];
    $alamat = $_POST['alamat'];
    $notelp = $_POST['notelp'];
    $email = $_POST['email'];
    $metode_pengambilan = $_POST['metode_pengambilan'];
    $tanggal_pengambilan = $_POST['tanggal_pengambilan'];

    // Handle upload file
    $nama_file = $_FILES['nama_file']['name'];
    $file_tmp = $_FILES['nama_file']['tmp_name'];
    $file_type = $_FILES['nama_file']['type'];

    // Tentukan lokasi penyimpanan file
    $upload_dir = '../dokumen/'; // Ubah sesuai dengan direktori penyimpanan Anda

    // Buat nama file unik untuk menghindari duplikasi
    $unique_file_name = uniqid() . '_' . $nama_file;

    // Pindahkan file ke direktori penyimpanan
    move_uploaded_file($file_tmp, $upload_dir . $unique_file_name);

    // Query untuk menyimpan data ke database
    $query = "INSERT INTO dokumen (id_user, nama_lengkap, alamat, notelp, email, metode_pengambilan, nama_file, tanggal_pengambilan) VALUES ('$id_user', '$nama_lengkap', '$alamat', '$notelp', '$email', '$metode_pengambilan', '$unique_file_name', '$tanggal_pengambilan')";

    if (mysqli_query($conn, $query)) {
        $script = "
                <script>
                    Swal.fire({
                        icon: 'success',
                        title: 'Dokumen berhasil dikirim!',
                        timer: 3000,
                        timerProgressBar: true,
                        showConfirmButton: false
                    });
                </script>
            ";
    } else {
        $script = "
                <script>
                    Swal.fire({
                        icon: 'error',
                        title: 'Dokumen Gagal Ditambahkan!',
                        timer: 3000,
                        timerProgressBar: true,
                        showConfirmButton: false
                    });
                </script>
            ";
    }
}



?>


<body id="page-top">

    <!-- Page Wrapper -->
    <div id="wrapper">

        <!-- Sidebar -->
        <?php include "sidebar.php"; ?>
        <!-- End of Sidebar -->

        <!-- Content Wrapper -->
        <div id="content-wrapper" class="d-flex flex-column">

            <!-- Main Content -->
            <div id="content">

                <!-- Topbar -->
                <?php include "topbar.php"; ?>
                <!-- End of Topbar -->

                <!-- Begin Page Content -->
                <div class="container-fluid">
                    <!-- DataTales Example -->
                    <div class="card shadow mb-4">
                        <div class="card-header py-3">
                            <h6 class="m-0 font-weight-bold text-primary">Dokumen Terkirim</h6>
                        </div>
                        <div class="card-body">
                            <div class="table-responsive">
                                <table class="table table-bordered" id="dataX" width="100%" cellspacing="0">
                                    <thead>
                                        <tr>
                                            <th>No</th>
                                            <th>Nama</th>
                                            <th>Alamat</th>
                                            <th>No Telp</th>
                                            <th>Email</th>
                                            <th>Metode Pengambilan</th>
                                            <th>File</th>
                                            <th>Tanggal Pengambilan</th>
                                        </tr>
                                    </thead>
                                    <tbody>
                                        <?php
                                        $dokumen = mysqli_query($conn, "SELECT * FROM dokumen WHERE id_user = '$id_user'");
                                        $i = 1;
                                        ?>
                                        <?php foreach ($dokumen as $td) : ?>
                                            <tr>
                                                <td><?= $i;
                                                    $i++; ?></td>
                                                <td><?= $td['nama_lengkap'] ?></td>
                                                <td><?= $td['alamat'] ?></td>
                                                <td><?= $td['notelp'] ?></td>
                                                <td><?= $td['email'] ?></td>
                                                <td><?= $td['metode_pengambilan'] ?></td>
                                                <td><a href="../dokumen/<?= $td['nama_file']; ?>" download="">Unduh File</a>
                                                </td>
                                                <td>
                                                    <?= date('d F, Y', strtotime($td['tanggal_pengambilan'])); ?>
                                                </td>
                                            </tr>
                                        <?php endforeach; ?>
                                    </tbody>
                                </table>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- /.container-fluid -->
                <!-- Modal Informasi Harga -->
                <div class="modal fade" id="hargaModal" tabindex="-1" role="dialog" aria-labelledby="myModalLabel" aria-hidden="true">
                    <div class="modal-dialog modal-lg">
                        <div class="modal-content">
                            <div class="modal-header">
                                <h4 class="modal-title" id="myModalLabel">Informasi Harga</h4>
                                <button type="button" class="close" data-dismiss="modal" aria-hidden="true">&times;</button>
                            </div>
                            <div class="modal-body">
                                <h5>Jasa yang disediakan:</h5>
                                <ol>
                                    <li>Photocopy: Rp. 400 / lembar</li>
                                    <li>Print:
                                        <ul>
                                            <li>biasa: Rp. 2.000 / lembar</li>
                                            <li>color: Rp. 3.000 / lembar</li>
                                            <li>full color: Rp. 6.000 / lembar</li>
                                        </ul>
                                    </li>
                                    <li>Jilid:
                                        <ul>
                                            <li>soft cover: Rp. 40.000</li>
                                            <li>spiral:
                                                <ul>
                                                    <li>plastik: Rp. 5.000</li>
                                                    <li>besi: Rp. 5.000</li>
                                                </ul>
                                            </li>
                                            <li>hard cover: Rp. 85.000</li>
                                        </ul>
                                    </li>
                                    <li>Laminating:
                                        <ul>
                                            <li>kartu: Rp. 3.000 / lembar</li>
                                            <li>dokumen A4: Rp. 6.000 / lembar</li>
                                            <li>dokumen F4: Rp. 7.000 / lembar</li>
                                        </ul>
                                    </li>
                                    <li>Scanning:
                                        <ul>
                                            <li>dokumen A4: Rp. 6.000 / lembar</li>
                                            <li>dokumen F4: Rp. 7.000 / lembar</li>
                                        </ul>
                                    </li>
                                    <li>Cetak Foto:
                                        <ul>
                                            <li>2x3: Rp. 3.000 / lembar</li>
                                            <li>3x4: Rp. 4.000 / lembar</li>
                                            <li>4x6: Rp. 5.000 / lembar</li>
                                            <li>4R: Rp. 5.000 / lembar</li>
                                        </ul>
                                    </li>
                                </ol>
                            </div>
                            <div class="modal-footer">
                                <button type="button" class="btn btn-default" data-dismiss="modal">Tutup</button>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- Modal Dokumen -->
                <div class="modal fade" id="dokumenModal" tabindex="-1" role="dialog" aria-labelledby="myModalLabel" aria-hidden="true">
                    <div class="modal-dialog modal-lg">
                        <div class="modal-content">
                            <div class="modal-header">
                                <h4 class="modal-title" id="myModalLabel">Kirim Dokumen</h4>
                                <button type="button" class="close" data-dismiss="modal" aria-hidden="true">&times;</button>
                            </div>
                            <div class="modal-body">
                                <form action="" method="POST" enctype="multipart/form-data">
                                    <label>Nama Lengkap</label>
                                    <input type="text" name="nama_lengkap" class="form-control">
                                    <label>Alamat</label>
                                    <input type="text" name="alamat" class="form-control">
                                    <label>No Telp</label>
                                    <input type="number" name="notelp" class="form-control">
                                    <label>Email</label>
                                    <input type="email" name="email" class="form-control">
                                    <label>Metode Pengambilan</label>
                                    <select name="metode_pengambilan" class="form-control">
                                        <option value="Diantar">Diantar</option>
                                        <option value="Ambil Sendiri">Ambil Sendiri</option>
                                    </select>
                                    <label>Dokumen/File</label>
                                    <input type="file" name="nama_file" class="form-control">
                                    <label>Tanggal Pengambilan</label>
                                    <input type="date" name="tanggal_pengambilan" class="form-control">
                                    <button type="submit" name="kirim" class="btn btn-success">Kirim</button>
                                </form>
                            </div>
                            <div class="modal-footer">
                                <button type="button" class="btn btn-default" data-dismiss="modal">Tutup</button>
                            </div>
                        </div>
                    </div>
                </div>


            </div>
            <!-- End of Main Content -->

            <!-- Footer -->
            <?php include "footer.php"; ?>
            <!-- End of Footer -->

        </div>
        <!-- End of Content Wrapper -->

    </div>
    <!-- End of Page Wrapper -->

    <!-- Scroll to Top Button-->
    <a class="scroll-to-top rounded" href="#page-top">
        <i class="fas fa-angle-up"></i>
    </a>

    <?php include "plugin.php"; ?>
    <?php
    if (isset($script)) {
        echo $script;
    }
    ?>

    <script>
        $(document).ready(function() {
            $('#dataX').DataTable({
                "language": {
                    "url": "//cdn.datatables.net/plug-ins/9dcbecd42ad/i18n/Indonesian.json",
                    "oPaginate": {
                        "sFirst": "Pertama",
                        "sLast": "Terakhir",
                        "sNext": "Selanjutnya",
                        "sPrevious": "Sebelumnya"
                    },
                    "sInfo": "Menampilkan _START_ sampai _END_ dari _TOTAL_ data",
                    "sSearch": "Cari:",
                    "sEmptyTable": "Tidak ada data yang tersedia dalam tabel",
                    "sLengthMenu": "Tampilkan _MENU_ data",
                    "sZeroRecords": "Tidak ada data yang cocok dengan pencarian Anda"
                }
            });
        });
    </script>
</body>

</html>

Footer
<footer class="sticky-footer bg-white" style="position: fixed; bottom:0; width:100%">
    <div class="container my-auto">
        <div class="copyright text-center my-auto">
            <span>Copyright &copy; SWIFT PRINT <?= date('Y'); ?></span>
        </div>
    </div>
</footer>

Link
<meta charset="utf-8">
<meta http-equiv="X-UA-Compatible" content="IE=edge">
<meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
<meta name="description" content="">
<meta name="author" content="">
<title>Swift Print</title>
<link rel="icon" href="../img/logo.png" type="image/x-icon">
<link href="../vendor/fontawesome-free/css/all.min.css" rel="stylesheet" type="text/css">
<link href="../css/sb-admin-2.min.css" rel="stylesheet">
<link href="../vendor/datatables/dataTables.bootstrap4.min.css" rel="stylesheet">
<link rel="stylesheet" href="../vendor/fontawesome-free/css/fontawesome.css">
<script src="../vendor/jquery/jquery.min.js"></script>
<link rel="stylesheet" href="../vendor/sweetalert2/dist/sweetalert2.min.css">
<?php

session_start();
include '../functions.php';
$id_user = $_SESSION['id_user'];

if (!isset($_SESSION["user"])) {
    header("Location: ../login.php");
    exit;
}

?>

Memilih Tempat
<!DOCTYPE html>
<html lang="en">

<head>
    <?php include "link.php"; ?>
</head>

<?php
// Jika form disubmit
if (isset($_POST['kirim'])) {
    // Ambil data dari form
    $nama_lengkap = $_POST['nama_lengkap'];
    $alamat = $_POST['alamat'];
    $notelp = $_POST['notelp'];
    $email = $_POST['email'];
    $metode_pengambilan = $_POST['metode_pengambilan'];
    $tanggal_pengambilan = $_POST['tanggal_pengambilan'];

    // Handle upload file
    $nama_file = $_FILES['nama_file']['name'];
    $file_tmp = $_FILES['nama_file']['tmp_name'];
    $file_type = $_FILES['nama_file']['type'];

    // Tentukan lokasi penyimpanan file
    $upload_dir = '../dokumen/'; // Ubah sesuai dengan direktori penyimpanan Anda

    // Buat nama file unik untuk menghindari duplikasi
    $unique_file_name = uniqid() . '_' . $nama_file;

    // Pindahkan file ke direktori penyimpanan
    move_uploaded_file($file_tmp, $upload_dir . $unique_file_name);

    // Query untuk menyimpan data ke database
    $query = "INSERT INTO dokumen (id_user, nama_lengkap, alamat, notelp, email, metode_pengambilan, nama_file, tanggal_pengambilan) VALUES ('$id_user', '$nama_lengkap', '$alamat', '$notelp', '$email', '$metode_pengambilan', '$unique_file_name', '$tanggal_pengambilan')";

    if (mysqli_query($conn, $query)) {
        $script = "
                <script>
                    Swal.fire({
                        icon: 'success',
                        title: 'Dokumen berhasil dikirim!',
                        timer: 3000,
                        timerProgressBar: true,
                        showConfirmButton: false
                    });
                </script>
            ";
    } else {
        $script = "
                <script>
                    Swal.fire({
                        icon: 'error',
                        title: 'Dokumen Gagal Ditambahkan!',
                        timer: 3000,
                        timerProgressBar: true,
                        showConfirmButton: false
                    });
                </script>
            ";
    }
}



?>


<body id="page-top">

    <!-- Page Wrapper -->
    <div id="wrapper">

        <!-- Sidebar -->
        <?php include "sidebar.php"; ?>
        <!-- End of Sidebar -->

        <!-- Content Wrapper -->
        <div id="content-wrapper" class="d-flex flex-column">

            <!-- Main Content -->
            <div id="content">

                <!-- Topbar -->
                <?php include "topbar.php"; ?>
                <!-- End of Topbar -->

                <!-- Begin Page Content -->
                <div class="container-fluid">
                    <!-- DataTales Example -->
                    <div class="card shadow mb-4">
                        <div class="card-header py-3">
                            <h6 class="m-0 font-weight-bold text-primary">Daftar Tempat</h6>
                        </div>
                        <div class="card-body">
                            <div class="table-responsive">
                                <table class="table table-bordered" id="dataX" width="100%" cellspacing="0">
                                    <thead>
                                        <tr>
                                            <th>No</th>
                                            <th>Nama</th>
                                            <th>Alamat</th>
                                            <th>Info</th>
                                            <th>Aksi</th>
                                        </tr>
                                    </thead>
                                    <tbody>
                                        <tr>
                                            <td>1</td>
                                            <td>OSLEN Photocopy & Printing</td>
                                            <td>
                                                Jl. Pendidikan No. 27, Kel. Klabulu, Malaimsimsa, Kota Sorong
                                            </td>
                                            <td>
                                                <button class="btn btn-info" data-toggle="modal" data-target="#hargaModal">Informasi Harga</button>
                                            </td>
                                            <td>
                                                <button class="btn btn-primary" data-toggle="modal" data-target="#dokumenModal">Kirim Dokumen</button>
                                            </td>
                                        </tr>
                                    </tbody>
                                </table>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- /.container-fluid -->
                <!-- Modal Informasi Harga -->
                <div class="modal fade" id="hargaModal" tabindex="-1" role="dialog" aria-labelledby="myModalLabel" aria-hidden="true">
                    <div class="modal-dialog modal-lg">
                        <div class="modal-content">
                            <div class="modal-header">
                                <h4 class="modal-title" id="myModalLabel">Informasi Harga</h4>
                                <button type="button" class="close" data-dismiss="modal" aria-hidden="true">&times;</button>
                            </div>
                            <div class="modal-body">
                                <h5>Jasa yang disediakan:</h5>
                                <ol>
                                    <li>Photocopy: Rp. 400 / lembar</li>
                                    <li>Print:
                                        <ul>
                                            <li>biasa: Rp. 2.000 / lembar</li>
                                            <li>color: Rp. 3.000 / lembar</li>
                                            <li>full color: Rp. 6.000 / lembar</li>
                                        </ul>
                                    </li>
                                    <li>Jilid:
                                        <ul>
                                            <li>soft cover: Rp. 40.000</li>
                                            <li>spiral:
                                                <ul>
                                                    <li>plastik: Rp. 5.000</li>
                                                    <li>besi: Rp. 5.000</li>
                                                </ul>
                                            </li>
                                            <li>hard cover: Rp. 85.000</li>
                                        </ul>
                                    </li>
                                    <li>Laminating:
                                        <ul>
                                            <li>kartu: Rp. 3.000 / lembar</li>
                                            <li>dokumen A4: Rp. 6.000 / lembar</li>
                                            <li>dokumen F4: Rp. 7.000 / lembar</li>
                                        </ul>
                                    </li>
                                    <li>Scanning:
                                        <ul>
                                            <li>dokumen A4: Rp. 6.000 / lembar</li>
                                            <li>dokumen F4: Rp. 7.000 / lembar</li>
                                        </ul>
                                    </li>
                                    <li>Cetak Foto:
                                        <ul>
                                            <li>2x3: Rp. 3.000 / lembar</li>
                                            <li>3x4: Rp. 4.000 / lembar</li>
                                            <li>4x6: Rp. 5.000 / lembar</li>
                                            <li>4R: Rp. 5.000 / lembar</li>
                                        </ul>
                                    </li>
                                </ol>
                            </div>
                            <div class="modal-footer">
                                <button type="button" class="btn btn-default" data-dismiss="modal">Tutup</button>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- Modal Dokumen -->
                <div class="modal fade" id="dokumenModal" tabindex="-1" role="dialog" aria-labelledby="myModalLabel" aria-hidden="true">
                    <div class="modal-dialog modal-lg">
                        <div class="modal-content">
                            <div class="modal-header">
                                <h4 class="modal-title" id="myModalLabel">Kirim Dokumen</h4>
                                <button type="button" class="close" data-dismiss="modal" aria-hidden="true">&times;</button>
                            </div>
                            <div class="modal-body">
                                <form action="" method="POST" enctype="multipart/form-data">
                                    <label>Nama Lengkap</label>
                                    <input type="text" name="nama_lengkap" class="form-control">
                                    <label>Alamat</label>
                                    <input type="text" name="alamat" class="form-control">
                                    <label>No Telp</label>
                                    <input type="number" name="notelp" class="form-control">
                                    <label>Email</label>
                                    <input type="email" name="email" class="form-control">
                                    <label>Metode Pengambilan</label>
                                    <select name="metode_pengambilan" class="form-control">
                                        <option value="Diantar">Diantar</option>
                                        <option value="Ambil Sendiri">Ambil Sendiri</option>
                                    </select>
                                    <label>Tambahkan File</label>
                                    <input type="file" name="nama_file" class="form-control">
                                    <label>Tanggal Pengambilan</label>
                                    <input type="date" name="tanggal_pengambilan" class="form-control"> <br>
                                    <button type="submit" name="kirim" class="btn btn-success w-100">Kirim</button>
                                </form>
                            </div>
                            <div class="modal-footer">
                                <button type="button" class="btn btn-default" data-dismiss="modal">Tutup</button>
                            </div>
                        </div>
                    </div>
                </div>


            </div>
            <!-- End of Main Content -->

            <!-- Footer -->
            <?php include "footer.php"; ?>
            <!-- End of Footer -->

        </div>
        <!-- End of Content Wrapper -->

    </div>
    <!-- End of Page Wrapper -->

    <!-- Scroll to Top Button-->
    <a class="scroll-to-top rounded" href="#page-top">
        <i class="fas fa-angle-up"></i>
    </a>

    <?php include "plugin.php"; ?>
    <?php
    if (isset($script)) {
        echo $script;
    }
    ?>

    <script>
        $(document).ready(function() {
            $('#dataX').DataTable({
                "language": {
                    "url": "//cdn.datatables.net/plug-ins/9dcbecd42ad/i18n/Indonesian.json",
                    "oPaginate": {
                        "sFirst": "Pertama",
                        "sLast": "Terakhir",
                        "sNext": "Selanjutnya",
                        "sPrevious": "Sebelumnya"
                    },
                    "sInfo": "Menampilkan _START_ sampai _END_ dari _TOTAL_ data",
                    "sSearch": "Cari:",
                    "sEmptyTable": "Tidak ada data yang tersedia dalam tabel",
                    "sLengthMenu": "Tampilkan _MENU_ data",
                    "sZeroRecords": "Tidak ada data yang cocok dengan pencarian Anda"
                }
            });
        });
    </script>
</body>

</html>

Plugin
<!-- Logout Modal-->
<div class="modal fade" id="logoutModal" tabindex="-1" role="dialog" aria-labelledby="exampleModalLabel" aria-hidden="true">
    <div class="modal-dialog" role="document">
        <div class="modal-content">
            <div class="modal-header">
                <h5 class="modal-title" id="exampleModalLabel">Yakin Ingin Logout?</h5>
                <button class="close" type="button" data-dismiss="modal" aria-label="Close">
                    <span aria-hidden="true">×</span>
                </button>
            </div>
            <div class="modal-body">Setelah <b>Logout</b>, untuk masuk ke sistem ini anda diharuskan <b>Login</b> terlebih.</div>
            <div class="modal-footer">
                <button class="btn btn-secondary" type="button" data-dismiss="modal">Cancel</button>
                <a class="btn btn-primary" href="../logout.php">Logout</a>
            </div>
        </div>
    </div>
</div>


<script src="../vendor/jquery/jquery.min.js"></script>
<script src="../vendor/bootstrap/js/bootstrap.bundle.min.js"></script>
<script src="../vendor/jquery-easing/jquery.easing.min.js"></script>
<script src="../js/sb-admin-2.min.js"></script>
<script src="../vendor/datatables/jquery.dataTables.min.js"></script>
<script src="../vendor/datatables/dataTables.bootstrap4.min.js"></script>
<script src="../vendor/chart.js/Chart.min.js"></script>
<script src="../js/demo/chart-area-demo.js"></script>
<script src="../js/demo/chart-pie-demo.js"></script>
<script src="../js/demo/datatables-demo.js"></script>
<script src="../vendor/sweetalert2/dist/sweetalert2.min.js"></script>

Sidebar
<ul class="navbar-nav bg-gradient-primary sidebar sidebar-dark accordion" id="accordionSidebar">

    <!-- Sidebar - Brand -->
    <a class="sidebar-brand d-flex align-items-center justify-content-center" href="index.php">
        <small>
            SWIFT PRINT <br>
            <i>User</i>
        </small>
    </a>

    <!-- Divider -->
    <hr class="sidebar-divider my-0">

    <!-- Nav Item  -->
    <li class="nav-item active">
        <a class="nav-link" href="index.php">
            <i class="fas fa-fw fa-home"></i>
            <span>Beranda</span></a>
    </li>

    <!-- Divider -->
    <hr class="sidebar-divider">


    <li class="nav-item active">
        <a class="nav-link collapsed" href="tentang_kami.php">
            <i class="fas fa-info"></i>
            <span>Tentang Kami</span>
        </a>
    </li>
    <li class="nav-item active">
        <a class="nav-link collapsed" href="memilih_tempat.php">
            <i class="fas fa-search"></i>
            <span>Memilih Tempat</span>
        </a>
    </li>
    <li class="nav-item active">
        <a class="nav-link collapsed" href="dokumen_terkirim.php">
            <i class="fas fa-envelope"></i>
            <span>Dokumen Terkirim</span>
        </a>
    </li>

    <!-- Divider -->
    <hr class="sidebar-divider">

    <!-- Sidebar Toggler (Sidebar) -->
    <div class="text-center d-none d-md-inline">
        <button class="rounded-circle border-0" id="sidebarToggle"></button>
    </div>

</ul>

Tentang Kami
<!DOCTYPE html>
<html lang="en">

<head>
    <?php include "link.php"; ?>
</head>

<body id="page-top">

    <!-- Page Wrapper -->
    <div id="wrapper">

        <!-- Sidebar -->
        <?php include "sidebar.php"; ?>
        <!-- End of Sidebar -->

        <!-- Content Wrapper -->
        <div id="content-wrapper" class="d-flex flex-column">

            <!-- Main Content -->
            <div id="content">

                <!-- Topbar -->
                <?php include "topbar.php"; ?>
                <!-- End of Topbar -->

                <!-- Begin Page Content -->
                <div class="container-fluid">

                    <!-- Page Heading -->
                    <div class="container w-100 mx-0">
                        <div class="card shadow mb-4">
                            <div class="card-header py-3">
                                <i>
                                    <h2 class="my-2 font-weight-bold text-primary">Tentang Swift Print</h2>
                                </i>
                                <h5 style="color:black !important">Swift Print adalah perusahaan cetak yang berfokus
                                    pada memberikan solusi cetak yang
                                    berkualitas tinggi, efisien, dan inovatif kepada pelanggan kami. Dibentuk pada tahun
                                    2010, kami telah mengukuhkan diri sebagai pemimpin dalam industri ini dengan
                                    berbagai penghargaan dan kepuasan pelanggan yang tinggi.
                                </h5>

                                <i>
                                    <h2 class="my-2 font-weight-bold text-primary">
                                        Misi Kami
                                    </h2>
                                </i>
                                <h5 style="color:black !important">
                                    Misi kami adalah menyediakan solusi cetak yang memenuhi berbagai kebutuhan, dari
                                    proyek
                                    kecil hingga kampanye besar, dengan kualitas yang tidak pernah berkurang. Kami
                                    bertekad
                                    untuk menciptakan pengalaman pelanggan yang positif dan membangun hubungan jangka
                                    panjang dengan Anda.
                                </h5>
                            </div>

                        </div>

                        <!-- Content Row -->

                    </div>
                    <!-- /.container-fluid -->

                </div>
                <!-- End of Main Content -->

                <!-- Footer -->
                <?php include "footer.php"; ?>
                <!-- End of Footer -->

            </div>
            <!-- End of Content Wrapper -->

        </div>
        <!-- End of Page Wrapper -->

        <!-- Scroll to Top Button-->
        <a class="scroll-to-top rounded" href="#page-top">
            <i class="fas fa-angle-up"></i>
        </a>

        <?php include "plugin.php"; ?>
</body>

</html>

Topbar
<nav class="navbar navbar-expand navbar-light bg-white topbar mb-4 static-top shadow">

    <!-- Sidebar Toggle (Topbar) -->
    <button id="sidebarToggleTop" class="btn btn-link d-md-none rounded-circle mr-3">
        <i class="fa fa-bars"></i>
    </button>

    <!-- Topbar Navbar -->
    <ul class="navbar-nav ml-auto">

        <!-- Nav Item - User Information -->
        <li class="nav-item dropdown no-arrow">
            <a class="nav-link dropdown-toggle" href="#" id="userDropdown" role="button" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
                <span class="mr-2 d-none d-lg-inline text-gray-600 small">Halo <?= $_SESSION['username']; ?> ! </span>
            </a>
            <!-- Dropdown - User Information -->
            <div class="dropdown-menu dropdown-menu-right shadow animated--grow-in" aria-labelledby="userDropdown">
                <a class="dropdown-item" href="../logout.php">
                    <i class="fas fa-sign-out-alt fa-sm fa-fw mr-2 text-gray-400"></i>
                    Logout
                </a>
            </div>
        </li>

    </ul>

</nav>

