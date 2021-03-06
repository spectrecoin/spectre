# SPDX-FileCopyrightText: © 2020 Alias Developers
# SPDX-FileCopyrightText: © 2019 SpectreCoin Developers
# SPDX-License-Identifier: MIT

##############################################################################
##### Some helper stuff ######################################################

# Configure a header file to pass some of the CMake settings
# to the source code like version and Git hash
configure_file(
        "${CMAKE_CURRENT_LIST_DIR}/clientversion.h.in"
        "${CMAKE_CURRENT_LIST_DIR}/clientversion.h"
)


##############################################################################
##### Setup a library with all the common content ############################

# Create dummy file since we want an empty shared library before linking
set(DUMMY_SOURCE ${CMAKE_BINARY_DIR}/dummy.c)
file(WRITE ${DUMMY_SOURCE} "")

add_library(aliaswallet_lib
        OBJECT
        ${DUMMY_SOURCE})

target_link_libraries(aliaswallet_lib
        Oracle::BerkeleyDB
        leveldb::leveldb
        OpenSSL::SSL
        OpenSSL::Crypto
        Boost::atomic
        Boost::boost
        Boost::chrono
        Boost::date_time
        Boost::filesystem
        Boost::iostreams
        Boost::program_options
        Boost::regex
        Boost::system
        Boost::thread
        )

target_include_directories(aliaswallet_lib
        SYSTEM BEFORE PUBLIC
        ${PROJECT_BINARY_DIR}/usr/local/include
        ${PROJECT_BINARY_DIR}/libdb/libdb-install/include
        ${OPENSSL_INCLUDE_DIR}
        ${BERKELEYDB_INCLUDE_DIR}
        ${LEVELDB_INCLUDE_DIR}
        )

# Common sources
target_sources(aliaswallet_lib
        PUBLIC
        ${CMAKE_CURRENT_LIST_DIR}/addrman.h
        ${CMAKE_CURRENT_LIST_DIR}/alert.h
        ${CMAKE_CURRENT_LIST_DIR}/allocators.h
        ${CMAKE_CURRENT_LIST_DIR}/anonymize.h
        ${CMAKE_CURRENT_LIST_DIR}/base58.h
        ${CMAKE_CURRENT_LIST_DIR}/bignum.h
        ${CMAKE_CURRENT_LIST_DIR}/bloom.h
        ${CMAKE_CURRENT_LIST_DIR}/chainparams.h
        ${CMAKE_CURRENT_LIST_DIR}/chainparamsseeds.h
        ${CMAKE_CURRENT_LIST_DIR}/checkpoints.h
        ${CMAKE_CURRENT_LIST_DIR}/clientversion.h
        ${CMAKE_CURRENT_LIST_DIR}/coincontrol.h
        ${CMAKE_CURRENT_LIST_DIR}/compat.h
        ${CMAKE_CURRENT_LIST_DIR}/core.h
        ${CMAKE_CURRENT_LIST_DIR}/crypter.h
        ${CMAKE_CURRENT_LIST_DIR}/db.h
        ${CMAKE_CURRENT_LIST_DIR}/eckey.h
        ${CMAKE_CURRENT_LIST_DIR}/extkey.h
        ${CMAKE_CURRENT_LIST_DIR}/hash.h
        ${CMAKE_CURRENT_LIST_DIR}/init.h
        ${CMAKE_CURRENT_LIST_DIR}/kernel.h
        ${CMAKE_CURRENT_LIST_DIR}/key.h
        ${CMAKE_CURRENT_LIST_DIR}/keystore.h
        ${CMAKE_CURRENT_LIST_DIR}/main.h
        ${CMAKE_CURRENT_LIST_DIR}/miner.h
        ${CMAKE_CURRENT_LIST_DIR}/mruset.h
        ${CMAKE_CURRENT_LIST_DIR}/netbase.h
        ${CMAKE_CURRENT_LIST_DIR}/net.h
        ${CMAKE_CURRENT_LIST_DIR}/pbkdf2.h
        ${CMAKE_CURRENT_LIST_DIR}/protocol.h
        ${CMAKE_CURRENT_LIST_DIR}/resource.h
        ${CMAKE_CURRENT_LIST_DIR}/ringsig.h
        ${CMAKE_CURRENT_LIST_DIR}/rpcclient.h
        ${CMAKE_CURRENT_LIST_DIR}/rpcprotocol.h
        ${CMAKE_CURRENT_LIST_DIR}/rpcserver.h
        ${CMAKE_CURRENT_LIST_DIR}/script.h
        ${CMAKE_CURRENT_LIST_DIR}/scrypt.h
        ${CMAKE_CURRENT_LIST_DIR}/serialize.h
        ${CMAKE_CURRENT_LIST_DIR}/smessage.h
        ${CMAKE_CURRENT_LIST_DIR}/state.h
        ${CMAKE_CURRENT_LIST_DIR}/stealth.h
        ${CMAKE_CURRENT_LIST_DIR}/strlcpy.h
        ${CMAKE_CURRENT_LIST_DIR}/sync.h
        ${CMAKE_CURRENT_LIST_DIR}/threadsafety.h
        ${CMAKE_CURRENT_LIST_DIR}/tinyformat.h
        ${CMAKE_CURRENT_LIST_DIR}/txdb.h
        ${CMAKE_CURRENT_LIST_DIR}/txdb-leveldb.h
        ${CMAKE_CURRENT_LIST_DIR}/txmempool.h
        ${CMAKE_CURRENT_LIST_DIR}/types.h
        ${CMAKE_CURRENT_LIST_DIR}/interface.h
        ${CMAKE_CURRENT_LIST_DIR}/uint256.h
        ${CMAKE_CURRENT_LIST_DIR}/util.h
        ${CMAKE_CURRENT_LIST_DIR}/version.h
        ${CMAKE_CURRENT_LIST_DIR}/walletdb.h
        ${CMAKE_CURRENT_LIST_DIR}/wallet.h
        ${CMAKE_CURRENT_LIST_DIR}/shutdown.h

        PRIVATE
        ${CMAKE_CURRENT_LIST_DIR}/addrman.cpp
        ${CMAKE_CURRENT_LIST_DIR}/alert.cpp
        ${CMAKE_CURRENT_LIST_DIR}/anonymize.cpp
        ${CMAKE_CURRENT_LIST_DIR}/bloom.cpp
        ${CMAKE_CURRENT_LIST_DIR}/chainparams.cpp
        ${CMAKE_CURRENT_LIST_DIR}/checkpoints.cpp
        ${CMAKE_CURRENT_LIST_DIR}/core.cpp
        ${CMAKE_CURRENT_LIST_DIR}/crypter.cpp
        ${CMAKE_CURRENT_LIST_DIR}/db.cpp
        ${CMAKE_CURRENT_LIST_DIR}/eckey.cpp
        ${CMAKE_CURRENT_LIST_DIR}/extkey.cpp
        ${CMAKE_CURRENT_LIST_DIR}/hash.cpp
        ${CMAKE_CURRENT_LIST_DIR}/init.cpp
        ${CMAKE_CURRENT_LIST_DIR}/kernel.cpp
        ${CMAKE_CURRENT_LIST_DIR}/key.cpp
        ${CMAKE_CURRENT_LIST_DIR}/keystore.cpp
        ${CMAKE_CURRENT_LIST_DIR}/main.cpp
        ${CMAKE_CURRENT_LIST_DIR}/miner.cpp
        ${CMAKE_CURRENT_LIST_DIR}/netbase.cpp
        ${CMAKE_CURRENT_LIST_DIR}/net.cpp
        ${CMAKE_CURRENT_LIST_DIR}/noui.cpp
        ${CMAKE_CURRENT_LIST_DIR}/pbkdf2.cpp
        ${CMAKE_CURRENT_LIST_DIR}/protocol.cpp
        ${CMAKE_CURRENT_LIST_DIR}/ringsig.cpp
        ${CMAKE_CURRENT_LIST_DIR}/rpcblockchain.cpp
        ${CMAKE_CURRENT_LIST_DIR}/rpcclient.cpp
        ${CMAKE_CURRENT_LIST_DIR}/rpcdump.cpp
        ${CMAKE_CURRENT_LIST_DIR}/rpcextkey.cpp
        ${CMAKE_CURRENT_LIST_DIR}/rpcmining.cpp
        ${CMAKE_CURRENT_LIST_DIR}/rpcmnemonic.cpp
        ${CMAKE_CURRENT_LIST_DIR}/rpcnet.cpp
        ${CMAKE_CURRENT_LIST_DIR}/rpcprotocol.cpp
        ${CMAKE_CURRENT_LIST_DIR}/rpcrawtransaction.cpp
        ${CMAKE_CURRENT_LIST_DIR}/rpcserver.cpp
        ${CMAKE_CURRENT_LIST_DIR}/rpcwallet.cpp
        ${CMAKE_CURRENT_LIST_DIR}/script.cpp
        ${CMAKE_CURRENT_LIST_DIR}/scrypt.cpp
        ${CMAKE_CURRENT_LIST_DIR}/smessage.cpp
        ${CMAKE_CURRENT_LIST_DIR}/state.cpp
        ${CMAKE_CURRENT_LIST_DIR}/stealth.cpp
        ${CMAKE_CURRENT_LIST_DIR}/sync.cpp
        ${CMAKE_CURRENT_LIST_DIR}/txdb-leveldb.cpp
        ${CMAKE_CURRENT_LIST_DIR}/txmempool.cpp
        ${CMAKE_CURRENT_LIST_DIR}/util.cpp
        ${CMAKE_CURRENT_LIST_DIR}/version.cpp
        ${CMAKE_CURRENT_LIST_DIR}/wallet.cpp
        ${CMAKE_CURRENT_LIST_DIR}/walletdb.cpp
        ${CMAKE_CURRENT_LIST_DIR}/shutdown.cpp
        )

add_subdirectory(json)
add_subdirectory(lz4)
add_subdirectory(wordlists)
add_subdirectory(xxhash)
if(CMAKE_SYSTEM_NAME STREQUAL "Windows")
    add_subdirectory(win)
endif ()



##############################################################################
##### Setup and link the executables #########################################


if (CMAKE_SYSTEM_NAME STREQUAL "Darwin")
    message(STATUS "No daemon build on Mac")
elseif(CMAKE_SYSTEM_NAME STREQUAL "Windows")
    message(STATUS "No daemon build on Windows")
else()
    # The daemon
    add_executable(Aliaswalletd ${CMAKE_CURRENT_LIST_DIR}/spectrecoind.cpp)

    # Link the daemon as static binary
    target_link_libraries(Aliaswalletd
            OpenSSL::SSL
            OpenSSL::Crypto
            Oracle::BerkeleyDB
            leveldb::leveldb
            aliaswallet_lib
            -static
            )
    set_target_properties(Aliaswalletd PROPERTIES
            OUTPUT_NAME aliaswalletd
            )
endif()

if (ENABLE_GUI)
    # The qm files are generated in the build tree, but the qrc file is inside the
    # source directory and the path to resources are relative to the location of
    # the qrc file itself. We use configure_file() to copy the qrc file in the build
    # directory such that it can find the qm translations files. The qrc file is
    # copied if it doesn't exist in the destination or if it is modified.
    configure_file(${CMAKE_CURRENT_SOURCE_DIR}/qt/alias_locale.qrc ${CMAKE_BINARY_DIR} COPYONLY)

    # Create only alias_en.ts new, to figure out if there are new strings to translate.
    # If src/qt/locale/alias_en.ts is modified afterwards, there are new strings to
    # translate. Any further steps on transifex.com.
    # Don't forget to add new source files here too, if they contain strings to translate!
    qt5_create_translation(QM_FILES
            ${CMAKE_CURRENT_LIST_DIR}/qt/forms/aboutdialog.ui
            ${CMAKE_CURRENT_LIST_DIR}/qt/forms/askpassphrasedialog.ui
            ${CMAKE_CURRENT_LIST_DIR}/qt/forms/coincontroldialog.ui
            ${CMAKE_CURRENT_LIST_DIR}/qt/forms/editaddressdialog.ui
            ${CMAKE_CURRENT_LIST_DIR}/qt/forms/rpcconsole.ui
            ${CMAKE_CURRENT_LIST_DIR}/qt/forms/transactiondescdialog.ui

            ${CMAKE_CURRENT_LIST_DIR}/qt/aboutdialog.h
            ${CMAKE_CURRENT_LIST_DIR}/qt/addresstablemodel.h
            ${CMAKE_CURRENT_LIST_DIR}/qt/aliasbridgestrings.h
            ${CMAKE_CURRENT_LIST_DIR}/qt/aliascorestrings.h
            ${CMAKE_CURRENT_LIST_DIR}/qt/askpassphrasedialog.h
            ${CMAKE_CURRENT_LIST_DIR}/qt/bitcoinaddressvalidator.h
            ${CMAKE_CURRENT_LIST_DIR}/qt/bitcoinamountfield.h
            ${CMAKE_CURRENT_LIST_DIR}/qt/bitcoinunits.h
            ${CMAKE_CURRENT_LIST_DIR}/qt/clientmodel.h
            ${CMAKE_CURRENT_LIST_DIR}/qt/coincontroldialog.h
            ${CMAKE_CURRENT_LIST_DIR}/qt/coincontroltreewidget.h
            ${CMAKE_CURRENT_LIST_DIR}/qt/csvmodelwriter.h
            ${CMAKE_CURRENT_LIST_DIR}/qt/editaddressdialog.h
            ${CMAKE_CURRENT_LIST_DIR}/qt/guiconstants.h
            ${CMAKE_CURRENT_LIST_DIR}/qt/guiutil.h
            ${CMAKE_CURRENT_LIST_DIR}/qt/monitoreddatamapper.h
            ${CMAKE_CURRENT_LIST_DIR}/qt/notificator.h
            ${CMAKE_CURRENT_LIST_DIR}/qt/optionsmodel.h
            ${CMAKE_CURRENT_LIST_DIR}/qt/paymentserver.h
            ${CMAKE_CURRENT_LIST_DIR}/qt/peertablemodel.h
            ${CMAKE_CURRENT_LIST_DIR}/qt/qvalidatedlineedit.h
            ${CMAKE_CURRENT_LIST_DIR}/qt/qvaluecombobox.h
            ${CMAKE_CURRENT_LIST_DIR}/qt/rpcconsole.h
            ${CMAKE_CURRENT_LIST_DIR}/qt/scicon.h
            ${CMAKE_CURRENT_LIST_DIR}/qt/setupwalletwizard.h
            ${CMAKE_CURRENT_LIST_DIR}/qt/spectrebridge.h
            ${CMAKE_CURRENT_LIST_DIR}/qt/spectregui.h
            ${CMAKE_CURRENT_LIST_DIR}/qt/trafficgraphwidget.h
            ${CMAKE_CURRENT_LIST_DIR}/qt/transactiondesc.h
            ${CMAKE_CURRENT_LIST_DIR}/qt/transactionrecord.h
            ${CMAKE_CURRENT_LIST_DIR}/qt/transactiontablemodel.h
            ${CMAKE_CURRENT_LIST_DIR}/qt/walletmodel.h
            ${CMAKE_CURRENT_LIST_DIR}/qt/websocketclientwrapper.h
            ${CMAKE_CURRENT_LIST_DIR}/qt/websockettransport.h

            ${CMAKE_CURRENT_LIST_DIR}/qt/aboutdialog.cpp
            ${CMAKE_CURRENT_LIST_DIR}/qt/addresstablemodel.cpp
            ${CMAKE_CURRENT_LIST_DIR}/qt/askpassphrasedialog.cpp
            ${CMAKE_CURRENT_LIST_DIR}/qt/bitcoinaddressvalidator.cpp
            ${CMAKE_CURRENT_LIST_DIR}/qt/bitcoinamountfield.cpp
            ${CMAKE_CURRENT_LIST_DIR}/qt/bitcoinunits.cpp
            ${CMAKE_CURRENT_LIST_DIR}/qt/clientmodel.cpp
            ${CMAKE_CURRENT_LIST_DIR}/qt/coincontroldialog.cpp
            ${CMAKE_CURRENT_LIST_DIR}/qt/coincontroltreewidget.cpp
            ${CMAKE_CURRENT_LIST_DIR}/qt/csvmodelwriter.cpp
            ${CMAKE_CURRENT_LIST_DIR}/qt/editaddressdialog.cpp
            ${CMAKE_CURRENT_LIST_DIR}/qt/guiutil.cpp
            ${CMAKE_CURRENT_LIST_DIR}/qt/monitoreddatamapper.cpp
            ${CMAKE_CURRENT_LIST_DIR}/qt/notificator.cpp
            ${CMAKE_CURRENT_LIST_DIR}/qt/optionsmodel.cpp
            ${CMAKE_CURRENT_LIST_DIR}/qt/paymentserver.cpp
            ${CMAKE_CURRENT_LIST_DIR}/qt/peertablemodel.cpp
            ${CMAKE_CURRENT_LIST_DIR}/qt/qvalidatedlineedit.cpp
            ${CMAKE_CURRENT_LIST_DIR}/qt/qvaluecombobox.cpp
            ${CMAKE_CURRENT_LIST_DIR}/qt/rpcconsole.cpp
            ${CMAKE_CURRENT_LIST_DIR}/qt/scicon.cpp
            ${CMAKE_CURRENT_LIST_DIR}/qt/setupwalletwizard.cpp
            ${CMAKE_CURRENT_LIST_DIR}/qt/spectrebridge.cpp
            ${CMAKE_CURRENT_LIST_DIR}/qt/spectregui.cpp
            ${CMAKE_CURRENT_LIST_DIR}/qt/trafficgraphwidget.cpp
            ${CMAKE_CURRENT_LIST_DIR}/qt/transactiondesc.cpp
            ${CMAKE_CURRENT_LIST_DIR}/qt/transactionrecord.cpp
            ${CMAKE_CURRENT_LIST_DIR}/qt/transactiontablemodel.cpp
            ${CMAKE_CURRENT_LIST_DIR}/qt/walletmodel.cpp
            ${CMAKE_CURRENT_LIST_DIR}/qt/websocketclientwrapper.cpp
            ${CMAKE_CURRENT_LIST_DIR}/qt/websockettransport.cpp
            ${CMAKE_CURRENT_LIST_DIR}/init.cpp
            ${CMAKE_CURRENT_LIST_DIR}/util.cpp
            ${CMAKE_CURRENT_LIST_DIR}/main.cpp
            ${CMAKE_CURRENT_LIST_DIR}/net.cpp
            ${CMAKE_CURRENT_LIST_DIR}/rpcserver.cpp
            ${CMAKE_CURRENT_LIST_DIR}/wallet.cpp

            ${CMAKE_CURRENT_LIST_DIR}/qt/locale/alias_en.ts
            )

    # Call lrelease on each translation file to create qm files.
    qt5_add_translation(QM_FILES
            ${CMAKE_CURRENT_SOURCE_DIR}/qt/locale/alias_af_ZA.ts
            ${CMAKE_CURRENT_SOURCE_DIR}/qt/locale/alias_ar.ts
            ${CMAKE_CURRENT_SOURCE_DIR}/qt/locale/alias_be.ts
            ${CMAKE_CURRENT_SOURCE_DIR}/qt/locale/alias_bg.ts
            ${CMAKE_CURRENT_SOURCE_DIR}/qt/locale/alias_bs.ts
            ${CMAKE_CURRENT_SOURCE_DIR}/qt/locale/alias_ca.ts
            ${CMAKE_CURRENT_SOURCE_DIR}/qt/locale/alias_ca@valencia.ts
            ${CMAKE_CURRENT_SOURCE_DIR}/qt/locale/alias_ca_ES.ts
            ${CMAKE_CURRENT_SOURCE_DIR}/qt/locale/alias_cs.ts
            ${CMAKE_CURRENT_SOURCE_DIR}/qt/locale/alias_cy.ts
            ${CMAKE_CURRENT_SOURCE_DIR}/qt/locale/alias_da.ts
            ${CMAKE_CURRENT_SOURCE_DIR}/qt/locale/alias_de.ts
            ${CMAKE_CURRENT_SOURCE_DIR}/qt/locale/alias_el.ts
            ${CMAKE_CURRENT_SOURCE_DIR}/qt/locale/alias_el_GR.ts
            ${CMAKE_CURRENT_SOURCE_DIR}/qt/locale/alias_eo.ts
            ${CMAKE_CURRENT_SOURCE_DIR}/qt/locale/alias_es.ts
            ${CMAKE_CURRENT_SOURCE_DIR}/qt/locale/alias_es_CL.ts
            ${CMAKE_CURRENT_SOURCE_DIR}/qt/locale/alias_es_DO.ts
            ${CMAKE_CURRENT_SOURCE_DIR}/qt/locale/alias_es_MX.ts
            ${CMAKE_CURRENT_SOURCE_DIR}/qt/locale/alias_es_UY.ts
            ${CMAKE_CURRENT_SOURCE_DIR}/qt/locale/alias_et.ts
            ${CMAKE_CURRENT_SOURCE_DIR}/qt/locale/alias_eu_ES.ts
            ${CMAKE_CURRENT_SOURCE_DIR}/qt/locale/alias_fa.ts
            ${CMAKE_CURRENT_SOURCE_DIR}/qt/locale/alias_fa_IR.ts
            ${CMAKE_CURRENT_SOURCE_DIR}/qt/locale/alias_fi.ts
            ${CMAKE_CURRENT_SOURCE_DIR}/qt/locale/alias_fr.ts
            ${CMAKE_CURRENT_SOURCE_DIR}/qt/locale/alias_fr_CA.ts
            ${CMAKE_CURRENT_SOURCE_DIR}/qt/locale/alias_gl.ts
            ${CMAKE_CURRENT_SOURCE_DIR}/qt/locale/alias_he.ts
            ${CMAKE_CURRENT_SOURCE_DIR}/qt/locale/alias_hi_IN.ts
            ${CMAKE_CURRENT_SOURCE_DIR}/qt/locale/alias_hr.ts
            ${CMAKE_CURRENT_SOURCE_DIR}/qt/locale/alias_hu.ts
            ${CMAKE_CURRENT_SOURCE_DIR}/qt/locale/alias_id_ID.ts
            ${CMAKE_CURRENT_SOURCE_DIR}/qt/locale/alias_it.ts
            ${CMAKE_CURRENT_SOURCE_DIR}/qt/locale/alias_ja.ts
            ${CMAKE_CURRENT_SOURCE_DIR}/qt/locale/alias_ka.ts
            ${CMAKE_CURRENT_SOURCE_DIR}/qt/locale/alias_kk.ts
            ${CMAKE_CURRENT_SOURCE_DIR}/qt/locale/alias_ko_KR.ts
            ${CMAKE_CURRENT_SOURCE_DIR}/qt/locale/alias_ky.ts
            ${CMAKE_CURRENT_SOURCE_DIR}/qt/locale/alias_la.ts
            ${CMAKE_CURRENT_SOURCE_DIR}/qt/locale/alias_lt.ts
            ${CMAKE_CURRENT_SOURCE_DIR}/qt/locale/alias_lv_LV.ts
            ${CMAKE_CURRENT_SOURCE_DIR}/qt/locale/alias_ms_MY.ts
            ${CMAKE_CURRENT_SOURCE_DIR}/qt/locale/alias_nb.ts
            ${CMAKE_CURRENT_SOURCE_DIR}/qt/locale/alias_nl.ts
            ${CMAKE_CURRENT_SOURCE_DIR}/qt/locale/alias_pam.ts
            ${CMAKE_CURRENT_SOURCE_DIR}/qt/locale/alias_pl.ts
            ${CMAKE_CURRENT_SOURCE_DIR}/qt/locale/alias_pt_BR.ts
            ${CMAKE_CURRENT_SOURCE_DIR}/qt/locale/alias_pt_PT.ts
            ${CMAKE_CURRENT_SOURCE_DIR}/qt/locale/alias_ro_RO.ts
            ${CMAKE_CURRENT_SOURCE_DIR}/qt/locale/alias_ru.ts
            ${CMAKE_CURRENT_SOURCE_DIR}/qt/locale/alias_sah.ts
            ${CMAKE_CURRENT_SOURCE_DIR}/qt/locale/alias_sk.ts
            ${CMAKE_CURRENT_SOURCE_DIR}/qt/locale/alias_sl_SI.ts
            ${CMAKE_CURRENT_SOURCE_DIR}/qt/locale/alias_sq.ts
            ${CMAKE_CURRENT_SOURCE_DIR}/qt/locale/alias_sr.ts
            ${CMAKE_CURRENT_SOURCE_DIR}/qt/locale/alias_sv.ts
            ${CMAKE_CURRENT_SOURCE_DIR}/qt/locale/alias_th.ts
            ${CMAKE_CURRENT_SOURCE_DIR}/qt/locale/alias_tr.ts
            ${CMAKE_CURRENT_SOURCE_DIR}/qt/locale/alias_uk.ts
            ${CMAKE_CURRENT_SOURCE_DIR}/qt/locale/alias_ur_PK.ts
            ${CMAKE_CURRENT_SOURCE_DIR}/qt/locale/alias_vi.ts
            ${CMAKE_CURRENT_SOURCE_DIR}/qt/locale/alias_vi_VN.ts
            ${CMAKE_CURRENT_SOURCE_DIR}/qt/locale/alias_zh_CN.ts
            ${CMAKE_CURRENT_SOURCE_DIR}/qt/locale/alias_zh_HK.ts
            ${CMAKE_CURRENT_SOURCE_DIR}/qt/locale/alias_zh_TW.ts
            )

    if (ANDROID)
        # Create a shared library 'libAliaswallet_<arch>.so'
        add_library(Aliaswallet
                SHARED
                ../spectre.qrc
                ${CMAKE_CURRENT_LIST_DIR}/qt/spectre.cpp
                ${CMAKE_BINARY_DIR}/alias_locale.qrc
                ${QM_FILES}
                )
#        set_target_properties(Aliaswallet
#                PROPERTIES
#                OUTPUT_NAME "Aliaswallet_${CMAKE_ANDROID_ARCH}"
#                )
        install(TARGETS Aliaswallet
            LIBRARY DESTINATION "${CMAKE_CURRENT_BINARY_DIR}/android-build/libs/${DCMAKE_ANDROID_ARCH_ABI}/"
            ARCHIVE DESTINATION "${CMAKE_CURRENT_BINARY_DIR}/android-build/libs/${DCMAKE_ANDROID_ARCH_ABI}/"
            )

        # Link the UI wallet
        # QtWebEngine not static available, so no static binary here :-(
        target_link_libraries(Aliaswallet
                OpenSSL::SSL
                OpenSSL::Crypto
                Oracle::BerkeleyDB
                leveldb::leveldb
                aliaswallet_lib
                Qt5::Core
                Qt5::Widgets
                Qt5::WebView
                Qt5::WebChannel
                Qt5::WebSockets
                Qt5::Quick
                Qt5::QuickWidgets
                Qt5::Svg
                Qt5::Concurrent
                )

        target_sources(Aliaswallet
                PUBLIC
                ${CMAKE_CURRENT_LIST_DIR}/qt/aboutdialog.h
                ${CMAKE_CURRENT_LIST_DIR}/qt/addresstablemodel.h
                ${CMAKE_CURRENT_LIST_DIR}/qt/aliasbridgestrings.h
                ${CMAKE_CURRENT_LIST_DIR}/qt/aliascorestrings.h
                ${CMAKE_CURRENT_LIST_DIR}/qt/askpassphrasedialog.h
                ${CMAKE_CURRENT_LIST_DIR}/qt/bitcoinaddressvalidator.h
                ${CMAKE_CURRENT_LIST_DIR}/qt/bitcoinamountfield.h
                ${CMAKE_CURRENT_LIST_DIR}/qt/bitcoinunits.h
                ${CMAKE_CURRENT_LIST_DIR}/qt/clientmodel.h
                ${CMAKE_CURRENT_LIST_DIR}/qt/coincontroldialog.h
                ${CMAKE_CURRENT_LIST_DIR}/qt/coincontroltreewidget.h
                ${CMAKE_CURRENT_LIST_DIR}/qt/csvmodelwriter.h
                ${CMAKE_CURRENT_LIST_DIR}/qt/editaddressdialog.h
                ${CMAKE_CURRENT_LIST_DIR}/qt/guiconstants.h
                ${CMAKE_CURRENT_LIST_DIR}/qt/guiutil.h
                ${CMAKE_CURRENT_LIST_DIR}/qt/monitoreddatamapper.h
                ${CMAKE_CURRENT_LIST_DIR}/qt/notificator.h
                ${CMAKE_CURRENT_LIST_DIR}/qt/optionsmodel.h
                ${CMAKE_CURRENT_LIST_DIR}/qt/paymentserver.h
                ${CMAKE_CURRENT_LIST_DIR}/qt/peertablemodel.h
                ${CMAKE_CURRENT_LIST_DIR}/qt/qvalidatedlineedit.h
                ${CMAKE_CURRENT_LIST_DIR}/qt/qvaluecombobox.h
                ${CMAKE_CURRENT_LIST_DIR}/qt/rpcconsole.h
                ${CMAKE_CURRENT_LIST_DIR}/qt/scicon.h
                ${CMAKE_CURRENT_LIST_DIR}/qt/setupwalletwizard.h
                ${CMAKE_CURRENT_LIST_DIR}/qt/spectrebridge.h
                ${CMAKE_CURRENT_LIST_DIR}/qt/spectregui.h
                ${CMAKE_CURRENT_LIST_DIR}/qt/trafficgraphwidget.h
                ${CMAKE_CURRENT_LIST_DIR}/qt/transactiondesc.h
                ${CMAKE_CURRENT_LIST_DIR}/qt/transactionrecord.h
                ${CMAKE_CURRENT_LIST_DIR}/qt/transactiontablemodel.h
                ${CMAKE_CURRENT_LIST_DIR}/qt/walletmodel.h
                ${CMAKE_CURRENT_LIST_DIR}/qt/websocketclientwrapper.h
                ${CMAKE_CURRENT_LIST_DIR}/qt/websockettransport.h

                PRIVATE
                ${CMAKE_CURRENT_LIST_DIR}/qt/aboutdialog.cpp
                ${CMAKE_CURRENT_LIST_DIR}/qt/addresstablemodel.cpp
                ${CMAKE_CURRENT_LIST_DIR}/qt/askpassphrasedialog.cpp
                ${CMAKE_CURRENT_LIST_DIR}/qt/bitcoinaddressvalidator.cpp
                ${CMAKE_CURRENT_LIST_DIR}/qt/bitcoinamountfield.cpp
                ${CMAKE_CURRENT_LIST_DIR}/qt/bitcoinunits.cpp
                ${CMAKE_CURRENT_LIST_DIR}/qt/clientmodel.cpp
                ${CMAKE_CURRENT_LIST_DIR}/qt/coincontroldialog.cpp
                ${CMAKE_CURRENT_LIST_DIR}/qt/coincontroltreewidget.cpp
                ${CMAKE_CURRENT_LIST_DIR}/qt/csvmodelwriter.cpp
                ${CMAKE_CURRENT_LIST_DIR}/qt/editaddressdialog.cpp
                ${CMAKE_CURRENT_LIST_DIR}/qt/guiutil.cpp
                ${CMAKE_CURRENT_LIST_DIR}/qt/monitoreddatamapper.cpp
                ${CMAKE_CURRENT_LIST_DIR}/qt/notificator.cpp
                ${CMAKE_CURRENT_LIST_DIR}/qt/optionsmodel.cpp
                ${CMAKE_CURRENT_LIST_DIR}/qt/paymentserver.cpp
                ${CMAKE_CURRENT_LIST_DIR}/qt/peertablemodel.cpp
                ${CMAKE_CURRENT_LIST_DIR}/qt/qvalidatedlineedit.cpp
                ${CMAKE_CURRENT_LIST_DIR}/qt/qvaluecombobox.cpp
                ${CMAKE_CURRENT_LIST_DIR}/qt/rpcconsole.cpp
                ${CMAKE_CURRENT_LIST_DIR}/qt/scicon.cpp
                ${CMAKE_CURRENT_LIST_DIR}/qt/setupwalletwizard.cpp
                ${CMAKE_CURRENT_LIST_DIR}/qt/spectrebridge.cpp
                ${CMAKE_CURRENT_LIST_DIR}/qt/spectregui.cpp
                ${CMAKE_CURRENT_LIST_DIR}/qt/trafficgraphwidget.cpp
                ${CMAKE_CURRENT_LIST_DIR}/qt/transactiondesc.cpp
                ${CMAKE_CURRENT_LIST_DIR}/qt/transactionrecord.cpp
                ${CMAKE_CURRENT_LIST_DIR}/qt/transactiontablemodel.cpp
                ${CMAKE_CURRENT_LIST_DIR}/qt/walletmodel.cpp
                ${CMAKE_CURRENT_LIST_DIR}/qt/websocketclientwrapper.cpp
                ${CMAKE_CURRENT_LIST_DIR}/qt/websockettransport.cpp
                )
    else()
        # The UI wallet
        if(CMAKE_SYSTEM_NAME STREQUAL "Darwin")
            # We have to reference the alias_locale.qrc copy in the build directory, not the
            # original file in the source directory. We also add qm files to the target to
            # create a dependency that will force rebuild in case the translation are
            # updated.
            add_executable(Aliaswallet
                    MACOSX_BUNDLE
                    ../spectre.qrc
                    ${CMAKE_CURRENT_LIST_DIR}/qt/spectre.cpp
                    ${CMAKE_BINARY_DIR}/alias_locale.qrc
                    ${QM_FILES}
                    )
        elseif (CMAKE_SYSTEM_NAME STREQUAL "Windows")
            # We have to reference the alias_locale.qrc copy in the build directory, not the
            # original file in the source directory. We also add qm files to the target to
            # create a dependency that will force rebuild in case the translation are
            # updated.
            add_executable(Aliaswallet
                    ../spectre.qrc
                    ${CMAKE_CURRENT_LIST_DIR}/qt/spectre.cpp
                    ${CMAKE_CURRENT_LIST_DIR}/qt/res/alias-qt.rc
                    ${CMAKE_BINARY_DIR}/alias_locale.qrc
                    ${QM_FILES}
                    )
        else()
            # We have to reference the alias_locale.qrc copy in the build directory, not the
            # original file in the source directory. We also add qm files to the target to
            # create a dependency that will force rebuild in case the translation are
            # updated.
            add_executable(Aliaswallet
                    ../spectre.qrc
                    ${CMAKE_CURRENT_LIST_DIR}/qt/spectre.cpp
                    ${CMAKE_BINARY_DIR}/alias_locale.qrc
                    ${QM_FILES}
                    )
        endif()

        # Link the UI wallet
        # QtWebEngine not static available, so no static binary here :-(
        target_link_libraries(Aliaswallet
                OpenSSL::SSL
                OpenSSL::Crypto
                Oracle::BerkeleyDB
                leveldb::leveldb
                aliaswallet_lib
                Qt5::Core
                Qt5::Widgets
                Qt5::WebView
                Qt5::WebChannel
                Qt5::WebSockets
                Qt5::Quick
                Qt5::QuickWidgets
                Qt5::Svg
                Qt5::Concurrent
                )

        target_sources(Aliaswallet
                PUBLIC
                ${CMAKE_CURRENT_LIST_DIR}/qt/aboutdialog.h
                ${CMAKE_CURRENT_LIST_DIR}/qt/addresstablemodel.h
                ${CMAKE_CURRENT_LIST_DIR}/qt/aliasbridgestrings.h
                ${CMAKE_CURRENT_LIST_DIR}/qt/aliascorestrings.h
                ${CMAKE_CURRENT_LIST_DIR}/qt/askpassphrasedialog.h
                ${CMAKE_CURRENT_LIST_DIR}/qt/bitcoinaddressvalidator.h
                ${CMAKE_CURRENT_LIST_DIR}/qt/bitcoinamountfield.h
                ${CMAKE_CURRENT_LIST_DIR}/qt/bitcoinunits.h
                ${CMAKE_CURRENT_LIST_DIR}/qt/clientmodel.h
                ${CMAKE_CURRENT_LIST_DIR}/qt/coincontroldialog.h
                ${CMAKE_CURRENT_LIST_DIR}/qt/coincontroltreewidget.h
                ${CMAKE_CURRENT_LIST_DIR}/qt/csvmodelwriter.h
                ${CMAKE_CURRENT_LIST_DIR}/qt/editaddressdialog.h
                ${CMAKE_CURRENT_LIST_DIR}/qt/guiconstants.h
                ${CMAKE_CURRENT_LIST_DIR}/qt/guiutil.h
                ${CMAKE_CURRENT_LIST_DIR}/qt/monitoreddatamapper.h
                ${CMAKE_CURRENT_LIST_DIR}/qt/notificator.h
                ${CMAKE_CURRENT_LIST_DIR}/qt/optionsmodel.h
                ${CMAKE_CURRENT_LIST_DIR}/qt/paymentserver.h
                ${CMAKE_CURRENT_LIST_DIR}/qt/peertablemodel.h
                ${CMAKE_CURRENT_LIST_DIR}/qt/qvalidatedlineedit.h
                ${CMAKE_CURRENT_LIST_DIR}/qt/qvaluecombobox.h
                ${CMAKE_CURRENT_LIST_DIR}/qt/rpcconsole.h
                ${CMAKE_CURRENT_LIST_DIR}/qt/scicon.h
                ${CMAKE_CURRENT_LIST_DIR}/qt/setupwalletwizard.h
                ${CMAKE_CURRENT_LIST_DIR}/qt/spectrebridge.h
                ${CMAKE_CURRENT_LIST_DIR}/qt/spectregui.h
                ${CMAKE_CURRENT_LIST_DIR}/qt/trafficgraphwidget.h
                ${CMAKE_CURRENT_LIST_DIR}/qt/transactiondesc.h
                ${CMAKE_CURRENT_LIST_DIR}/qt/transactionrecord.h
                ${CMAKE_CURRENT_LIST_DIR}/qt/transactiontablemodel.h
                ${CMAKE_CURRENT_LIST_DIR}/qt/walletmodel.h
                ${CMAKE_CURRENT_LIST_DIR}/qt/websocketclientwrapper.h
                ${CMAKE_CURRENT_LIST_DIR}/qt/websockettransport.h

                PRIVATE
                ${CMAKE_CURRENT_LIST_DIR}/qt/aboutdialog.cpp
                ${CMAKE_CURRENT_LIST_DIR}/qt/addresstablemodel.cpp
                ${CMAKE_CURRENT_LIST_DIR}/qt/askpassphrasedialog.cpp
                ${CMAKE_CURRENT_LIST_DIR}/qt/bitcoinaddressvalidator.cpp
                ${CMAKE_CURRENT_LIST_DIR}/qt/bitcoinamountfield.cpp
                ${CMAKE_CURRENT_LIST_DIR}/qt/bitcoinunits.cpp
                ${CMAKE_CURRENT_LIST_DIR}/qt/clientmodel.cpp
                ${CMAKE_CURRENT_LIST_DIR}/qt/coincontroldialog.cpp
                ${CMAKE_CURRENT_LIST_DIR}/qt/coincontroltreewidget.cpp
                ${CMAKE_CURRENT_LIST_DIR}/qt/csvmodelwriter.cpp
                ${CMAKE_CURRENT_LIST_DIR}/qt/editaddressdialog.cpp
                ${CMAKE_CURRENT_LIST_DIR}/qt/guiutil.cpp
                ${CMAKE_CURRENT_LIST_DIR}/qt/monitoreddatamapper.cpp
                ${CMAKE_CURRENT_LIST_DIR}/qt/notificator.cpp
                ${CMAKE_CURRENT_LIST_DIR}/qt/optionsmodel.cpp
                ${CMAKE_CURRENT_LIST_DIR}/qt/paymentserver.cpp
                ${CMAKE_CURRENT_LIST_DIR}/qt/peertablemodel.cpp
                ${CMAKE_CURRENT_LIST_DIR}/qt/qvalidatedlineedit.cpp
                ${CMAKE_CURRENT_LIST_DIR}/qt/qvaluecombobox.cpp
                ${CMAKE_CURRENT_LIST_DIR}/qt/rpcconsole.cpp
                ${CMAKE_CURRENT_LIST_DIR}/qt/scicon.cpp
                ${CMAKE_CURRENT_LIST_DIR}/qt/setupwalletwizard.cpp
                ${CMAKE_CURRENT_LIST_DIR}/qt/spectrebridge.cpp
                ${CMAKE_CURRENT_LIST_DIR}/qt/spectregui.cpp
                ${CMAKE_CURRENT_LIST_DIR}/qt/trafficgraphwidget.cpp
                ${CMAKE_CURRENT_LIST_DIR}/qt/transactiondesc.cpp
                ${CMAKE_CURRENT_LIST_DIR}/qt/transactionrecord.cpp
                ${CMAKE_CURRENT_LIST_DIR}/qt/transactiontablemodel.cpp
                ${CMAKE_CURRENT_LIST_DIR}/qt/walletmodel.cpp
                ${CMAKE_CURRENT_LIST_DIR}/qt/websocketclientwrapper.cpp
                ${CMAKE_CURRENT_LIST_DIR}/qt/websockettransport.cpp
                )

        if(CMAKE_SYSTEM_NAME STREQUAL "Darwin")
            target_sources(Aliaswallet
                PUBLIC
                ${CMAKE_CURRENT_LIST_DIR}/qt/macdockiconhandler.h
                ${CMAKE_CURRENT_LIST_DIR}/qt/macnotificationhandler.h
                PRIVATE
                ${CMAKE_CURRENT_LIST_DIR}/qt/macdockiconhandler.mm
                ${CMAKE_CURRENT_LIST_DIR}/qt/macnotificationhandler.mm
                )
            set_target_properties(Aliaswallet PROPERTIES
                MACOSX_BUNDLE_INFO_STRING "${PROJECT_NAME}${DBG_EXTENSION} Version ${VERSION_STRING}, © 2020 The Alias developers."
                MACOSX_BUNDLE_GUI_IDENTIFIER "${PROJECT_NAME}${DBG_EXTENSION}"
                MACOSX_BUNDLE_LONG_VERSION_STRING "${PROJECT_NAME}${DBG_EXTENSION} Version ${VERSION_STRING}"
                MACOSX_BUNDLE_BUNDLE_NAME ${PROJECT_NAME}${DBG_EXTENSION}
                MACOSX_BUNDLE_SHORT_VERSION_STRING ${VERSION_STRING}
                MACOSX_BUNDLE_BUNDLE_VERSION ${VERSION_STRING}
                MACOSX_BUNDLE_COPYRIGHT " © 2020 The Alias developers"
                MACOSX_BUNDLE_INFO_PLIST ${CMAKE_CURRENT_LIST_DIR}/osx/MacOSXBundleInfo.plist.in
                OUTPUT_NAME Alias
                )
            target_link_libraries(Aliaswallet "-framework AppKit")
            add_custom_command(TARGET Aliaswallet POST_BUILD
#                    COMMAND cd ${CMAKE_BINARY_DIR} && "${MACDEPLOYQT_EXECUTABLE}"
#                    Alias.app
#                    -qmldir=${CMAKE_SOURCE_DIR}/src/qt/res
#                    -always-overwrite
#                    -verbose=1
#                    ${DEPLOY_QT_BINARY_TYPE_OPTION}
                    COMMAND rm -rf ${CMAKE_BINARY_DIR}/Alias.app/Contents/MacOS/Tor
                    COMMAND unzip ${TOR_ARCHIVE} -d ${CMAKE_BINARY_DIR}/Alias.app/
                    COMMAND chmod +x ${CMAKE_BINARY_DIR}/Alias.app/Contents/MacOS/Tor/tor.real
                    COMMAND chmod +x ${CMAKE_BINARY_DIR}/Alias.app/Contents/MacOS/Tor/libevent*
                    COMMAND chmod +x ${CMAKE_BINARY_DIR}/Alias.app/Contents/MacOS/Tor/PluggableTransports/*
                    COMMAND mkdir -p ${CMAKE_BINARY_DIR}/Alias.app/Contents/Resources
                    COMMAND cp ${CMAKE_SOURCE_DIR}/src/qt/res/icons/alias-app.icns ${CMAKE_BINARY_DIR}/Alias.app/Contents/Resources/
#                    COMMAND cd ${CMAKE_BINARY_DIR} && "${MACDEPLOYQT_EXECUTABLE}"
#                    Alias.app
#                    -dmg
#                    -always-overwrite
#                    -verbose=1
                    COMMENT "Put additional content onto app directory"
                    )
        elseif(CMAKE_SYSTEM_NAME STREQUAL "Windows")
            target_sources(Aliaswallet
                PUBLIC
                ${CMAKE_CURRENT_LIST_DIR}/qt/winshutdownmonitor.h
                PRIVATE
                ${CMAKE_CURRENT_LIST_DIR}/qt/winshutdownmonitor.cpp
                )
            set_target_properties(Aliaswallet PROPERTIES
                    OUTPUT_NAME Alias
                    )
            target_link_libraries(Aliaswallet "Shlwapi")
            add_custom_command(TARGET Aliaswallet POST_BUILD
                    COMMAND ${CMAKE_COMMAND} -E remove_directory ${CMAKE_BINARY_DIR}/Alias
                    COMMAND "${CMAKE_COMMAND}" -E
                    env PATH="${_qt_bin_dir}" "${WINDEPLOYQT_EXECUTABLE}"
                    --force
                    --libdir ${CMAKE_BINARY_DIR}/delivery
                    --plugindir ${CMAKE_BINARY_DIR}/delivery
                    ${DEPLOY_QT_BINARY_TYPE_OPTION}
                    --qmldir ${CMAKE_SOURCE_DIR}/src/qt/res/qml
                    --qml
                    --quick
                    --webengine
                    "$<TARGET_FILE:Aliaswallet>"
                    COMMAND unzip -o ${VCRUNTIME_ARCHIVE} -d ${CMAKE_BINARY_DIR}/delivery/
                    COMMAND unzip -o ${TOR_ARCHIVE} -d ${CMAKE_BINARY_DIR}/delivery/
                    COMMAND ${CMAKE_COMMAND} -E copy_directory ${CMAKE_BINARY_DIR}/delivery/Release/ ${CMAKE_BINARY_DIR}/delivery/
                    COMMAND ${CMAKE_COMMAND} -E remove_directory ${CMAKE_BINARY_DIR}/delivery/Release
                    COMMAND ${CMAKE_COMMAND} -E rename ${CMAKE_BINARY_DIR}/delivery ${CMAKE_BINARY_DIR}/Alias
                    COMMENT "Running windeployqt..."
                    )
        else()
            set_target_properties(Aliaswallet PROPERTIES
                    OUTPUT_NAME aliaswallet
                    )
        endif()
    endif()
endif ()

#message(STATUS "BERKELEYDB_INCLUDE_PATH: ${BERKELEYDB_INCLUDE_PATH}")
#message(STATUS "OPENSSL_INCLUDE_PATH: ${OPENSSL_INCLUDE_PATH}")
#message(STATUS "OPENSSL_API_COMPAT: ${OPENSSL_API_COMPAT}")
