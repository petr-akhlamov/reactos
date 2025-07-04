add_subdirectory(makeimg)

list(APPEND SOURCE
    AttachThreadInput.c
    ../include/msgtrace.c
    CharFuncs.c
    CloseWindow.c
    CopyImage.c
    CreateDialog.c
    CreateIconFromResourceEx.c
    CreateWindowEx.c
    DeferWindowPos.c
    DestroyCursorIcon.c
    DM_REPOSITION.c
    DrawIconEx.c
    DrawText.c
    desktop.c
    EmptyClipboard.c
    EnumDisplaySettings.c
    GetClassInfo.c
    GetDCEx.c
    GetIconInfo.c
    GetKeyState.c
    GetMessageTime.c
    GetPeekMessage.c
    GetSetWindowInt.c
    GetSystemMetrics.c
    GetUserObjectInformation.c
    GetWindowPlacement.c
    GW_ENABLEDPOPUP.c
    InitializeLpkHooks.c
    KbdLayout.c
    keybd_event.c
    LoadImage.c
    LoadImageGCC.c
    LookupIconIdFromDirectoryEx.c
    MenuUI.c
    MessageStateAnalyzer.c
    NextDlgItem.c
    PrivateExtractIcons.c
    RealGetWindowClass.c
    RedrawWindow.c
    RegisterClassEx.c
    RegisterHotKey.c
    ScrollBarRedraw.c
    ScrollBarWndExtra.c
    ScrollDC.c
    ScrollWindowEx.c
    SendMessageTimeout.c
    SetActiveWindow.c
    SetCursorPos.c
    SetFocus.c
    SetParent.c
    SetProp.c
    SetScrollInfo.c
    SetScrollRange.c
    SetWindowPlacement.c
    ShowWindow.c
    SwitchToThisWindow.c
    SystemMenu.c
    SystemParametersInfo.c
    TrackMouseEvent.c
    TrackPopupMenuEx.c
    VirtualKey.c
    WndProc.c
    wsprintf.c)

list(APPEND PCH_SKIP_SOURCE
    testlist.c)

add_executable(user32_apitest
    ${SOURCE}
    ${PCH_SKIP_SOURCE}
    user32_apitest.rc)

target_link_libraries(user32_apitest wine ${PSEH_LIB})
set_module_type(user32_apitest win32cui)
add_importlibs(user32_apitest advapi32 imm32 gdi32 user32 msvcrt kernel32 ntdll)
add_pch(user32_apitest precomp.h "${PCH_SKIP_SOURCE}")
add_rostests_file(TARGET user32_apitest)

add_executable(user32_apitest_menuui user32_apitest_menuui.c)
set_module_type(user32_apitest_menuui win32gui UNICODE)
add_importlibs(user32_apitest_menuui user32 msvcrt kernel32)
add_rostests_file(TARGET user32_apitest_menuui)
add_dependencies(user32_apitest user32_apitest_menuui)

add_rostests_file(FILE "${CMAKE_CURRENT_SOURCE_DIR}/verclasstest1.manifest")
add_rostests_file(FILE "${CMAKE_CURRENT_SOURCE_DIR}/verclasstest2.manifest")
