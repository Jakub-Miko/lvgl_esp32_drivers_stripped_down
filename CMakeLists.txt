if(ESP_PLATFORM)

file(GLOB SOURCES *.c)

set(LVGL_INCLUDE_DIRS . lvgl_tft)
list(APPEND SOURCES "lvgl_tft/disp_driver.c")
list(APPEND SOURCES "lvgl_tft/esp_lcd_backlight.c")

list(APPEND SOURCES "lvgl_tft/ili9163c.c")

list(APPEND SOURCES "lvgl_tft/disp_spi.c")

idf_component_register(SRCS ${SOURCES}
                       INCLUDE_DIRS ${LVGL_INCLUDE_DIRS}
                       REQUIRES lvgl esp_driver_spi esp_driver_gpio esp_driver_i2c esp_driver_ledc driver)

target_compile_definitions(${COMPONENT_LIB} PUBLIC "-DLV_LVGL_H_INCLUDE_SIMPLE")

else()
    message(FATAL_ERROR "LVGL ESP32 drivers: ESP_PLATFORM is not defined. Try reinstalling ESP-IDF.")
endif()
