# Change Log

All notable changes to this project will be documented in this file.
See [Conventional Commits](https://conventionalcommits.org) for commit guidelines.

# [7.0.0](https://github.com/waitingsong/node-win32-api/compare/v6.2.0...v7.0.0) (2019-12-23)


### Bug Fixes

* 'PVOID' not parsed within parse_windef() ([3209b6c](https://github.com/waitingsong/node-win32-api/commit/3209b6cf0c076eba58e94c8d5904e0baa77a87d5))
* LPBYTE ([70cadc1](https://github.com/waitingsong/node-win32-api/commit/70cadc18909b1e9b6e8c3c5b819ba99d93aa7ee2))
* missing file marcomap.ts ([692efbc](https://github.com/waitingsong/node-win32-api/commit/692efbc914a6ae241b218db0374e2edf3010b321))
* struct not parsed ([0df3999](https://github.com/waitingsong/node-win32-api/commit/0df3999278ee589d0ed58cce7e55b3517f4bee52))
* USN ([a246d16](https://github.com/waitingsong/node-win32-api/commit/a246d16214a1bf4cdc6c58510b6682f1e2222a91))
* **types:** parse_windef() ([03de209](https://github.com/waitingsong/node-win32-api/commit/03de209cecdf55e4b374fc1c276918e36975cb37))


### chore

* **deps:** use ffi-napi instead of ffi ([bfa006c](https://github.com/waitingsong/node-win32-api/commit/bfa006c468e93813cfedce68eb2e94fd901058cc))


### Features

* add FILETIME structure ([2482e79](https://github.com/waitingsong/node-win32-api/commit/2482e79b6497c9e037c64596b9d0d15250bebb6e))
* **types:** add DllFuncsModel ([d4b258b](https://github.com/waitingsong/node-win32-api/commit/d4b258b12a799b4e0846c16430a9f106c8b129be))
* **types:** change ReturnType of cb of async() from void to any ([1f69876](https://github.com/waitingsong/node-win32-api/commit/1f6987645dd303d29cde962a44db5d06bc051b8c))
* **types:** expand exported DllFuncsModel with async() method ([2cf076a](https://github.com/waitingsong/node-win32-api/commit/2cf076a290eca73e0b76eb3a87dce921eaab254c))
* **types:** set below [@deprecated](https://github.com/deprecated) ([d480b4b](https://github.com/waitingsong/node-win32-api/commit/d480b4bc5af4ba30335adfb8206fb3979a466bba))
* add HARDWAREINPUT, HARDWAREINPUT_Struct ([3ae64f3](https://github.com/waitingsong/node-win32-api/commit/3ae64f35e64a4e7fbe5184fbb5bcd822cfd1743d))
* add isPathAcessible() ([01810da](https://github.com/waitingsong/node-win32-api/commit/01810da580cd4791dd8041ee1d18adb0d48381ef))
* add KEYBDINPUT, KEYBDINPUT_Struct ([8ca6f3f](https://github.com/waitingsong/node-win32-api/commit/8ca6f3f8f1d1797a8e61499959d9aeef93b4d29a))
* add LoadSettings['singleton'] ([9be9d53](https://github.com/waitingsong/node-win32-api/commit/9be9d53e7378fa14c250c8feb0bca2499959eb4e))
* add logger() ([fe705c5](https://github.com/waitingsong/node-win32-api/commit/fe705c517be2557ba11fb332ca64ffc232d906ee))
* add LPPOINT ([d85e0a7](https://github.com/waitingsong/node-win32-api/commit/d85e0a7c92eef6a08944f4982ae83316ce520ad8))
* add MOUSEINPUT, MOUSEINPUT_Struct ([60fb063](https://github.com/waitingsong/node-win32-api/commit/60fb0630c8020a94dea1e3040939ed7bd986536f))
* add RAWHID, RAWHID_Struct ([2e5d09e](https://github.com/waitingsong/node-win32-api/commit/2e5d09e59c06929c909e695113dedee4382a6632))
* add RAWINPUTHEADER, RAWINPUTHEADER_Struct ([ca557fa](https://github.com/waitingsong/node-win32-api/commit/ca557fafb7c6d048df928df4b807cb9c85c62c51))
* add RAWKEYBOARD, RAWKEYBOARD_Struct ([9a3c56b](https://github.com/waitingsong/node-win32-api/commit/9a3c56bc3272ab226746be4008e6ebe79d840194))
* change types of VOID to number & Buffer & void ([e129f16](https://github.com/waitingsong/node-win32-api/commit/e129f16783545aa8946b2134d0d17c491787220a))
* copy from node-win32-api and update ([5e290b1](https://github.com/waitingsong/node-win32-api/commit/5e290b133dbe804c93b9aaf25b84af75087fc763))
* export basename() from shared ([a5ffb0b](https://github.com/waitingsong/node-win32-api/commit/a5ffb0b5dbf61d370df893fa423d60806d62fcf5))
* export FModel.Buffer as alias of FModel.FFIBuffer ([2a36d0f](https://github.com/waitingsong/node-win32-api/commit/2a36d0f715e2423dab184c7544cfd03a21867753))
* export os.tmpdir() ([c98a3ab](https://github.com/waitingsong/node-win32-api/commit/c98a3ab84c6898d00dad5ee8a266ea860d937722))
* rename export name of ww to dataTypes ([baf5a52](https://github.com/waitingsong/node-win32-api/commit/baf5a521ef6cba908e04e75ee94ca3109e752f63))
* structure instance has ref() member for ref-struct ([2b2b48e](https://github.com/waitingsong/node-win32-api/commit/2b2b48e7511d2311ade0f4d361c75ad98de96179))
* use lookupRef() instead of retrieve_ref_value() ([e1f9497](https://github.com/waitingsong/node-win32-api/commit/e1f9497a89250b502af1de33cb2d03f70cdd1cb1))
* **types:** change FFIParam to FnParam ([8176abe](https://github.com/waitingsong/node-win32-api/commit/8176abe8aa7d9adfb5baa7cab1c5981b82cd844a))


### Reverts

* to 84d3d698a5b1 ([d94d128](https://github.com/waitingsong/node-win32-api/commit/d94d12889154547c9e73feca05c4a84c3e2f50d8))


### BREAKING CHANGES

* **deps:** remove nodejs v8 support





# Change Log

All notable changes to this project will be documented in this file. See [standard-version](https://github.com/conventional-changelog/standard-version) for commit guidelines.

# [3.3.0](https://github.com/waitingsong/node-win32-def/compare/v3.2.0...v3.3.0) (2019-03-17)


### Features

* add FILETIME structure ([4da430f](https://github.com/waitingsong/node-win32-def/commit/4da430f))



<a name="2.4.3"></a>
## [2.4.3](https://github.com/waitingsong/node-win32-def/compare/v2.4.2...v2.4.3) (2019-02-21)


### Bug Fixes

* createDir() path resolve under linux ([c6d1274](https://github.com/waitingsong/node-win32-def/commit/c6d1274))


### Features

* add Observable functions ([c9364db](https://github.com/waitingsong/node-win32-def/commit/c9364db))
* do isPathAccessible() first within isDirFileExists() ([9ddae98](https://github.com/waitingsong/node-win32-def/commit/9ddae98))
* export statAsync ([c832590](https://github.com/waitingsong/node-win32-def/commit/c832590))