
README FILE FOR BUILDING AND COMPILING THE AGILE PROJECT AS A PURE C++ PROJECT

Instructions

1. In the top directory create a build directory (somepath/your_repository/)
when you create build it will be: somepath/your_repository/build
2. Go into the build directory just created 
3. Run $ cmake .. 
This will build the project into the build directory by calling the CMakeLists.txt that is in the main directory
4. Do $ls and make sure that now you have files in your build directory
5. Run $ make
This will compile the whole dependencies and libraries
6. Once this compiled successfully, there will be a TestCPP executable. It can be run as follows:
$ ./TestCPP your_path_to_repository/repository_name/your_file.pcd your_path_to_repository/repository_name/svm_file

EXAMPLE:

There are two *.pcd files for testing and many svm files in the top directory. To use them and run TestCPP you can do the following:

$./TestCPP your_path_to_repository/repository_name/clusterTest.pcd your_path_to_repository/repository_name/svm_032015_20_20_same

Another example assuming my path is ~ and repository name is agile_grasp

$./TestCPP ~/agile_grasp/clusterTest.pcd ~/agile_grasp/svm_032015_20_20_same
