afr_module()

afr_module_sources(
    pkcs11
    PRIVATE "${AFR_MODULES_DIR}/include/aws_pkcs11.h"
)

afr_module_include_dirs(
    pkcs11
    PUBLIC
        "${AFR_MODULES_DIR}/include"
        "${AFR_MODULES_DIR}/include/private"
)

afr_module_dependencies(
    pkcs11
    PUBLIC
        3rdparty::pkcs11
    PRIVATE
        AFR::pkcs11::mcu_port
)


# Link to this INTERFACE target to use the default implementation based on mbedtls.
afr_module(NAME pkcs11_mbedtls INTERFACE)
afr_module_sources(
    pkcs11_mbedtls INTERFACE
    "${AFR_MODULES_DIR}/pkcs11/mbedtls/aws_pkcs11_mbedtls.c"
    "${AFR_MODULES_DIR}/include/private/threading_alt.h"
)
afr_module_dependencies(
    pkcs11_mbedtls INTERFACE
    AFR::crypto
    3rdparty::mbedtls
)
