cmake_minimum_required(VERSION 3.10.0 FATAL_ERROR)
project(XP-Qt)
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTOUIC ON)
set(CMAKE_AUTORCC ON)

set(CMAKE_VERBOSE_MAKEFILE ON)

find_package(Qt5 CONFIG COMPONENTS Core Widgets Network REQUIRED NO_DEFAULT_PATH)
message("Qt5_FOUND: ${Qt5_FOUND}")
message("Qt5_DIR: ${Qt5_DIR}")

find_package(Boost 1.65 EXACT COMPONENTS system filesystem thread program_options)
if (NOT Boost_FOUND)
   message(FATAL_ERROR "Please give hints by BOOST_ROOT")
endif()
message("Boost_FOUND: ${Boost_FOUND}")
message("Boost_INCLUDE_DIRS: ${Boost_INCLUDE_DIRS}")
message("Boost_LIBRARY_DIRS: ${Boost_LIBRARY_DIRS}")
message("Boost_LIBRARIES: ${Boost_LIBRARIES}")

if (NOT OpenSSL_DIR)
   message(FATAL_ERROR "Please specify OpenSSL_DIR")
endif()
message("OpenSSL_DIR: ${OpenSSL_DIR}")

if (NOT BerkeleyDB_INCDIR)
   message(FATAL_ERROR "Please specify BerkeleyDB_INCDIR")
endif()
if (NOT BerkeleyDB_LIBDIR)
   message(FATAL_ERROR "Please specify BerkeleyDB_LIBDIR")
endif()
message("BerkeleyDB_INCDIR: ${BerkeleyDB_INCDIR}")
message("BerkeleyDB_LIBDIR: ${BerkeleyDB_LIBDIR}")


add_executable(xp-qt
   src/qt/bitcoin.cpp
   src/qt/bitcoingui.cpp
   src/qt/intro.cpp
   src/qt/transactiontablemodel.cpp
   src/qt/addresstablemodel.cpp
   src/qt/optionsdialog.cpp
   src/qt/sendcoinsdialog.cpp
   src/qt/coincontroldialog.cpp
   src/qt/coincontroltreewidget.cpp
   src/qt/addressbookpage.cpp
   src/qt/signverifymessagedialog.cpp
   src/qt/aboutdialog.cpp
   src/qt/editaddressdialog.cpp
   src/qt/bitcoinaddressvalidator.cpp
   src/qt/trafficgraphwidget.cpp
   src/qt/mintingfilterproxy.cpp
   src/qt/mintingtablemodel.cpp
   src/qt/mintingview.cpp
   src/kernelrecord.cpp
   src/alert.cpp
   src/version.cpp
   src/sync.cpp
   src/util.cpp
   src/netbase.cpp
   src/ntp.cpp
   src/key.cpp
   src/script.cpp
   src/main.cpp
   src/miner.cpp
   src/init.cpp
   src/net.cpp
   src/stun.cpp
   src/irc.cpp
   src/checkpoints.cpp
   src/addrman.cpp
   src/db.cpp
   src/walletdb.cpp
   src/qt/clientmodel.cpp
   src/qt/guiutil.cpp
   src/qt/transactionrecord.cpp
   src/qt/optionsmodel.cpp
   src/qt/monitoreddatamapper.cpp
   src/qt/transactiondesc.cpp
   src/qt/transactiondescdialog.cpp
   src/qt/bitcoinstrings.cpp
   src/qt/bitcoinamountfield.cpp
   src/wallet.cpp
   src/keystore.cpp
   src/qt/transactionfilterproxy.cpp
   src/qt/transactionview.cpp
   src/qt/walletmodel.cpp
   src/bitcoinrpc.cpp
   src/rpcdump.cpp
   src/rpcnet.cpp
   src/rpcmining.cpp
   src/rpcwallet.cpp
   src/rpcblockchain.cpp
   src/rpcrawtransaction.cpp
   src/qt/overviewpage.cpp
   src/qt/csvmodelwriter.cpp
   src/crypter.cpp
   src/qt/sendcoinsentry.cpp
   src/qt/qvalidatedlineedit.cpp
   src/qt/bitcoinunits.cpp
   src/qt/qvaluecombobox.cpp
   src/qt/askpassphrasedialog.cpp
   src/protocol.cpp
   src/qt/notificator.cpp
   src/qt/qtipcserver.cpp
   src/qt/rpcconsole.cpp
   src/noui.cpp
   src/kernel.cpp
   src/kernel_worker.cpp
   src/qt/multisigaddressentry.cpp
   src/qt/multisiginputentry.cpp
   src/qt/multisigdialog.cpp
   src/qt/secondauthdialog.cpp
   src/qt/qrcodedialog.cpp
   src/base58.cpp
   src/qt/bitcoin.qrc
   src/txdb-bdb.cpp
   #src/crypto/scrypt/generic/scrypt-generic.cpp
   )

target_compile_definitions(xp-qt
   PRIVATE QT_GUI BOOST_THREAD_USE_LIB BOOST_SPIRIT_THREADSAFE __STDC_FORMAT_MACROS __STDC_LIMIT_MACROS
   )
target_include_directories(xp-qt
   PRIVATE
   ${PROJECT_SOURCE_DIR}/src
   ${PROJECT_SOURCE_DIR}/src/json
   ${PROJECT_SOURCE_DIR}/src/qt
   ${OpenSSL_DIR}/include
   ${BerkeleyDB_INCDIR}
   )
target_link_directories(xp-qt
   PRIVATE
   ${OpenSSL_DIR}/lib
   ${BerkeleyDB_LIBDIR}
   )
target_link_libraries(xp-qt
   #db-4.8 db_cxx-4.8
   db-5.3 db_cxx-5.3
   ssl crypto
   pthread rt
   qrencode
   Boost::system Boost::thread Boost::filesystem Boost::program_options
   Qt5::Core Qt5::Widgets Qt5::Network
   )
set_property(TARGET xp-qt PROPERTY AUTOUIC_SEARCH_PATHS 
   src/qt/forms
   )

set_property(SOURCE
   src/wallet.h
   src/alert.cpp
   src/bitcoinrpc.cpp
   src/db.cpp
   src/init.cpp
   src/main.cpp
   src/net.cpp
   src/noui.cpp
   src/ntp.cpp
   src/qt/bitcoin.cpp
   src/qt/bitcoingui.cpp
   src/qt/clientmodel.cpp
   src/qt/qtipcserver.cpp
   src/qt/transactiondesc.cpp
   src/qt/transactiontablemodel.cpp
   src/qt/walletmodel.cpp
   src/rpcdump.cpp
   src/util.cpp
   src/wallet.cpp
   PROPERTY SKIP_AUTOUIC ON
   )

