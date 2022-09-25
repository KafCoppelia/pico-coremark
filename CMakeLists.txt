if (TARGET tinyusb_device)
    include_directories("coremark")
    aux_source_directory(. src_coremark)
    add_executable(coremark ${src_coremark})

    # pull in common dependencies
    target_link_libraries(coremark pico_stdlib)
    pico_set_binary_type(coremark no_flash)

    # enable usb output, disable uart output
    pico_enable_stdio_usb(coremark 1)
    pico_enable_stdio_uart(coremark 0)

    # create map/bin/hex file etc.
    pico_add_extra_outputs(coremark)

elseif(PICO_ON_DEVICE)
    message(WARNING "not building coremark because TinyUSB submodule is not initialized in the SDK")
endif()