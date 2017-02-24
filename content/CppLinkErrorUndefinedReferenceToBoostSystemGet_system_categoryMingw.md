

[Go back to Richel Bilderbeek's C++ page](Cpp.htm).

 

 

 

 

 

([C++](Cpp.htm)) [Undefined reference to 'boost::system::get\_system\_category()' (using MinGW)](CppLinkErrorUndefinedReferenceToBoostSystemGet_system_categoryMingw.htm)
=========================================================================================================================================================================

 

[Link error](CppLinkError.htm) ([BEI](CppBei.htm) 6) I encountered while
busy solving [How to cross-compile a Qt Creator project from Ubuntu to a
windows executable: example 3: console application with a Boost
library](CppQtCrosscompileToWindowsExample3.htm).

 

-   [Download the source code of
    'CppLinkErrorUndefinedReferenceToBoostSystemGet\_system\_categoryMingw' (zip)](CppLinkErrorUndefinedReferenceToBoostSystemGet_system_categoryMingw.zip)

 

 

 

 

 

 

System specifics
----------------

 

Operating system: [Ubuntu](http://www.ubuntu.com) 10.04 LTS Lucid Lynx

[IDE](CppIde.htm): gedit

 

 

 

 

 

Source code: main.cpp
---------------------

 

  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include <iostream> #include <string> #include <vector> //--------------------------------------------------------------------------- #include <boost/filesystem.hpp> //--------------------------------------------------------------------------- //From http://www.richelbilderbeek.nl/CppGetFilesInFolder.htm const std::vector<std::string> GetFilesInFolder(const std::string& folder) {   std::vector<std::string> v;    const boost::filesystem::path my_folder     = boost::filesystem::system_complete(         boost::filesystem::path(folder));    if (!boost::filesystem::is_directory(my_folder)) return v;    const boost::filesystem::directory_iterator j;   for ( boost::filesystem::directory_iterator i(my_folder);         i != j;         ++i)   {     if ( boost::filesystem::is_regular_file( i->status() ) )     {       const std::string filename = i->path().filename();       //const std::string full_filename = folder + "/" + filename;       v.push_back(filename);     }   }   return v; } //--------------------------------------------------------------------------- //From http://www.richelbilderbeek.nl/CppGetPath.htm const std::string GetPath(const std::string& filename) {   return boost::filesystem::path(filename).parent_path().string(); } //--------------------------------------------------------------------------- int main(int, char* argv[]) {   const std::vector<std::string> v = GetFilesInFolder(GetPath(argv[0]));   std::copy(v.begin(),v.end(),std::ostream_iterator<std::string>(std::cout,"\n"));   std::cout << "Number of files: " << v.size() << '\n'; } //---------------------------------------------------------------------------`
  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

Process
-------

 

Because I was trying to solve the [Qt FAQ](CppQtFaq.htm) [How to
cross-compile a Qt Creator project from Ubuntu to a windows
executable?](CppQtCrosscompileToWindows.htm), I compiled the code as
follows:

 

  -------------------------------------------------------------------------------------------------------------
  ` i586-mingw32msvc-g++ -o MyWin.exe main.cpp -I/usr/i586-mingw32msvc/include -L/usr/lib -lboost_filesystem`
  -------------------------------------------------------------------------------------------------------------

 

This results in the following screen output:

 

  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ``  /tmp/ccUkpKJv.o:main.cpp:(.text+0x138): undefined reference to 'boost::system::get_system_category()' /tmp/ccUkpKJv.o:main.cpp:(.text+0x142): undefined reference to `boost::system::get_generic_category()' /tmp/ccUkpKJv.o:main.cpp:(.text+0x14c): undefined reference to `boost::system::get_generic_category()' /tmp/ccUkpKJv.o:main.cpp:(.text+0x156): undefined reference to `boost::system::get_generic_category()' /tmp/ccUkpKJv.o:main.cpp:(.text+0x160): undefined reference to `boost::system::get_system_category()' /tmp/ccUkpKJv.o:main.cpp:(.text$_ZN5boost6system10error_codeC1Ev[boost::system::error_code::error_code()]+0x10): undefined reference to `boost::system::get_system_category()' /tmp/ccUkpKJv.o:main.cpp:(.text$_ZN5boost10filesystem15system_completeINS0_10basic_pathISsNS0_11path_traitsEEEEENS_9enable_ifINS0_13is_basic_pathIT_EES7_E4typeERKS7_[boost::enable_if<boost::filesystem::is_basic_path<boost::filesystem::basic_path<std::basic_string<char, std::char_traits<char>, std::allocator<char> >, boost::filesystem::path_traits> >, boost::filesystem::basic_path<std::basic_string<char, std::char_traits<char>, std::allocator<char> >, boost::filesystem::path_traits> >::type boost::filesystem::system_complete<boost::filesystem::basic_path<std::basic_string<char, std::char_traits<char>, std::allocator<char> >, boost::filesystem::path_traits> >(boost::filesystem::basic_path<std::basic_string<char, std::char_traits<char>, std::allocator<char> >, boost::filesystem::path_traits> const&)]+0xae): undefined reference to `boost::filesystem::detail::get_full_path_name_api(std::basic_string<char, std::char_traits<char>, std::allocator<char> > const&, std::basic_string<char, std::char_traits<char>, std::allocator<char> >&)' /tmp/ccUkpKJv.o:main.cpp:(.text$_ZN5boost10filesystem12is_directoryINS0_10basic_pathISsNS0_11path_traitsEEEEENS_9enable_ifINS0_13is_basic_pathIT_EEbE4typeERKS7_[boost::enable_if<boost::filesystem::is_basic_path<boost::filesystem::basic_path<std::basic_string<char, std::char_traits<char>, std::allocator<char> >, boost::filesystem::path_traits> >, bool>::type boost::filesystem::is_directory<boost::filesystem::basic_path<std::basic_string<char, std::char_traits<char>, std::allocator<char> >, boost::filesystem::path_traits> >(boost::filesystem::basic_path<std::basic_string<char, std::char_traits<char>, std::allocator<char> >, boost::filesystem::path_traits> const&)]+0x77): undefined reference to `boost::filesystem::detail::status_api(std::basic_string<char, std::char_traits<char>, std::allocator<char> > const&, boost::system::error_code&)' /tmp/ccUkpKJv.o:main.cpp:(.text$_ZN5boost10filesystem6statusINS0_10basic_pathISsNS0_11path_traitsEEEEENS_9enable_ifINS0_13is_basic_pathIT_EENS0_11file_statusEE4typeERKS7_[boost::enable_if<boost::filesystem::is_basic_path<boost::filesystem::basic_path<std::basic_string<char, std::char_traits<char>, std::allocator<char> >, boost::filesystem::path_traits> >, boost::filesystem::file_status>::type boost::filesystem::status<boost::filesystem::basic_path<std::basic_string<char, std::char_traits<char>, std::allocator<char> >, boost::filesystem::path_traits> >(boost::filesystem::basic_path<std::basic_string<char, std::char_traits<char>, std::allocator<char> >, boost::filesystem::path_traits> const&)]+0x77): undefined reference to `boost::filesystem::detail::status_api(std::basic_string<char, std::char_traits<char>, std::allocator<char> > const&, boost::system::error_code&)' /tmp/ccUkpKJv.o:main.cpp:(.text$_ZN5boost10filesystem6detail11dir_itr_impINS0_10basic_pathISsNS0_11path_traitsEEEED1Ev[boost::filesystem::detail::dir_itr_imp<boost::filesystem::basic_path<std::basic_string<char, std::char_traits<char>, std::allocator<char> >, boost::filesystem::path_traits> >::~dir_itr_imp()]+0x4b): undefined reference to `boost::filesystem::detail::dir_itr_close(void*&)' /tmp/ccUkpKJv.o:main.cpp:(.text$_ZN5boost10filesystem24basic_directory_iteratorINS0_10basic_pathISsNS0_11path_traitsEEEE9incrementEv[boost::filesystem::basic_directory_iterator<boost::filesystem::basic_path<std::basic_string<char, std::char_traits<char>, std::allocator<char> >, boost::filesystem::path_traits> >::increment()]+0x103): undefined reference to `boost::filesystem::detail::dir_itr_increment(void*&, std::basic_string<char, std::char_traits<char>, std::allocator<char> >&, boost::filesystem::file_status&, boost::filesystem::file_status&)' /tmp/ccUkpKJv.o:main.cpp:(.text$_ZN5boost10filesystem24basic_directory_iteratorINS0_10basic_pathISsNS0_11path_traitsEEEE6m_initERKS4_[boost::filesystem::basic_directory_iterator<boost::filesystem::basic_path<std::basic_string<char, std::char_traits<char>, std::allocator<char> >, boost::filesystem::path_traits> >::m_init(boost::filesystem::basic_path<std::basic_string<char, std::char_traits<char>, std::allocator<char> >, boost::filesystem::path_traits> const&)]+0x65): undefined reference to `boost::filesystem::detail::not_found_error()' /tmp/ccUkpKJv.o:main.cpp:(.text$_ZN5boost10filesystem24basic_directory_iteratorINS0_10basic_pathISsNS0_11path_traitsEEEE6m_initERKS4_[boost::filesystem::basic_directory_iterator<boost::filesystem::basic_path<std::basic_string<char, std::char_traits<char>, std::allocator<char> >, boost::filesystem::path_traits> >::m_init(boost::filesystem::basic_path<std::basic_string<char, std::char_traits<char>, std::allocator<char> >, boost::filesystem::path_traits> const&)]+0xf3): undefined reference to `boost::filesystem::detail::dir_itr_first(void*&, std::basic_string<char, std::char_traits<char>, std::allocator<char> > const&, std::basic_string<char, std::char_traits<char>, std::allocator<char> >&, boost::filesystem::file_status&, boost::filesystem::file_status&)' ``
  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

Improving the call to the one below, does not remove the error.

 

` i586-mingw32msvc-g++ -o MyWin.exe main.cpp -I/usr/i586-mingw32msvc/include -L/usr/lib -lboost_filesystem -lboost_system `

 

I suspect that the Windows version of the Boost libraries must be copied
to '/usr/i586-mingw32msvc/lib'.

 

I tried 'Failed attempt \#1'.

 

Also ruthlessly copying some Boost Windows lib files to
'usr/i586-mingw32msvc/lib' and 'usr/i586-mingw32msvc/lib/boost' failed.

 

 

 

 

 

Failed attempt \#1: just copy those files from the Ubuntu computer
------------------------------------------------------------------

 

I noted that '/usr/i586-mingw32msvc/lib' contained libraries with a '.a'
extension. In '/usr/lib', I can find boost\_filesystem.a and
boost\_system.a. I try to copy them ruthlessly:

 

` sudo cp /usr/lib/libboost_system.a /usr/i586-mingw32msvc/lib/ sudo cp /usr/lib/libboost_filesystem.a /usr/i586-mingw32msvc/lib/ `

 

Perhaps in a '/usr/i586-mingw32msvc/lib/boost' folder?

 

` sudo mkdir /usr/i586-mingw32msvc/lib/boost sudo cp /usr/lib/libboost_system.a /usr/i586-mingw32msvc/lib/boost sudo cp /usr/lib/libboost_filesystem.a /usr/i586-mingw32msvc/lib/boost `

 

 

Set the library path to the new one:

 

` i586-mingw32msvc-g++ -o MyWin.exe main.cpp -I/usr/i586-mingw32msvc/include -L/usr/i586-mingw32msvc/lib -lboost_filesystem -lboost_system `

 

This approach does not work.

 

 

 

 

[Go back to Richel Bilderbeek's C++ page](Cpp.htm).



 

[![Valid XHTML 1.0 Strict](valid-xhtml10.png){width="88"
height="31"}](http://validator.w3.org/check?uri=referer)