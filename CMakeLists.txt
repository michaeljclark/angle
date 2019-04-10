# Copyright 2019 The ANGLE Project Authors. All rights reserved.

cmake_minimum_required(VERSION 3.0)

project(angle)

########################################################################
#
# ANGLE Source and header variables
#
########################################################################

set(angle_translator_sources
  include/EGL/egl.h
  include/EGL/eglext.h
  include/EGL/eglplatform.h
  include/GLES2/gl2.h
  include/GLES2/gl2ext.h
  include/GLES2/gl2platform.h
  include/GLES3/gl3.h
  include/GLES3/gl3platform.h
  include/GLES3/gl31.h
  include/GLES3/gl32.h
  include/GLSLANG/ShaderLang.h
  include/GLSLANG/ShaderVars.h
  include/KHR/khrplatform.h
  include/angle_gl.h
  src/compiler/translator/BaseTypes.h
  src/compiler/translator/BuiltInFunctionEmulator.cpp
  src/compiler/translator/BuiltInFunctionEmulator.h
  src/compiler/translator/CallDAG.cpp
  src/compiler/translator/CallDAG.h
  src/compiler/translator/CodeGen.cpp
  src/compiler/translator/CollectVariables.cpp
  src/compiler/translator/CollectVariables.h
  src/compiler/translator/Common.h
  src/compiler/translator/Compiler.cpp
  src/compiler/translator/Compiler.h
  src/compiler/translator/ConstantUnion.cpp
  src/compiler/translator/ConstantUnion.h
  src/compiler/translator/Declarator.cpp
  src/compiler/translator/Declarator.h
  src/compiler/translator/Diagnostics.cpp
  src/compiler/translator/Diagnostics.h
  src/compiler/translator/DirectiveHandler.cpp
  src/compiler/translator/DirectiveHandler.h
  src/compiler/translator/ExtensionBehavior.cpp
  src/compiler/translator/ExtensionBehavior.h
  src/compiler/translator/FlagStd140Structs.cpp
  src/compiler/translator/FlagStd140Structs.h
  src/compiler/translator/FunctionLookup.cpp
  src/compiler/translator/FunctionLookup.h
  src/compiler/translator/HashNames.cpp
  src/compiler/translator/HashNames.h
  src/compiler/translator/ImmutableString.cpp
  src/compiler/translator/ImmutableString.h
  src/compiler/translator/ImmutableStringBuilder.cpp
  src/compiler/translator/ImmutableStringBuilder.h
  src/compiler/translator/InfoSink.cpp
  src/compiler/translator/InfoSink.h
  src/compiler/translator/Initialize.cpp
  src/compiler/translator/Initialize.h
  src/compiler/translator/InitializeDll.cpp
  src/compiler/translator/InitializeDll.h
  src/compiler/translator/InitializeGlobals.h
  src/compiler/translator/IntermNode.h
  src/compiler/translator/IntermNode.cpp
  src/compiler/translator/IsASTDepthBelowLimit.cpp
  src/compiler/translator/IsASTDepthBelowLimit.h
  src/compiler/translator/Operator.cpp
  src/compiler/translator/Operator.h
  src/compiler/translator/OutputTree.cpp
  src/compiler/translator/OutputTree.h
  src/compiler/translator/ParseContext.cpp
  src/compiler/translator/ParseContext.h
  src/compiler/translator/ParseContext_autogen.h
  src/compiler/translator/PoolAlloc.cpp
  src/compiler/translator/PoolAlloc.h
  src/compiler/translator/Pragma.h
  src/compiler/translator/QualifierTypes.h
  src/compiler/translator/QualifierTypes.cpp
  src/compiler/translator/Severity.h
  src/compiler/translator/ShaderLang.cpp
  src/compiler/translator/ShaderVars.cpp
  src/compiler/translator/StaticType.h
  src/compiler/translator/Symbol.cpp
  src/compiler/translator/Symbol.h
  src/compiler/translator/SymbolTable.cpp
  src/compiler/translator/SymbolTable.h
  src/compiler/translator/SymbolTable_autogen.cpp
  src/compiler/translator/SymbolTable_autogen.h
  src/compiler/translator/SymbolUniqueId.cpp
  src/compiler/translator/SymbolUniqueId.h
  src/compiler/translator/Types.cpp
  src/compiler/translator/Types.h
  src/compiler/translator/ValidateAST.cpp
  src/compiler/translator/ValidateAST.h
  src/compiler/translator/ValidateGlobalInitializer.cpp
  src/compiler/translator/ValidateGlobalInitializer.h
  src/compiler/translator/ValidateLimitations.cpp
  src/compiler/translator/ValidateLimitations.h
  src/compiler/translator/ValidateMaxParameters.h
  src/compiler/translator/ValidateMaxParameters.cpp
  src/compiler/translator/ValidateOutputs.cpp
  src/compiler/translator/ValidateOutputs.h
  src/compiler/translator/ValidateSwitch.cpp
  src/compiler/translator/ValidateSwitch.h
  src/compiler/translator/ValidateVaryingLocations.cpp
  src/compiler/translator/ValidateVaryingLocations.h
  src/compiler/translator/VariablePacker.cpp
  src/compiler/translator/VariablePacker.h
  src/compiler/translator/blocklayout.cpp
  src/compiler/translator/blocklayout.h
  src/compiler/translator/glslang.h
  src/compiler/translator/glslang.l
  src/compiler/translator/glslang.y
  src/compiler/translator/glslang_lex.cpp
  src/compiler/translator/glslang_tab.cpp
  src/compiler/translator/glslang_tab.h
  src/compiler/translator/length_limits.h
  src/compiler/translator/util.cpp
  src/compiler/translator/util.h
  src/compiler/translator/tree_ops/AddAndTrueToLoopCondition.cpp
  src/compiler/translator/tree_ops/AddAndTrueToLoopCondition.h
  src/compiler/translator/tree_ops/BreakVariableAliasingInInnerLoops.cpp
  src/compiler/translator/tree_ops/BreakVariableAliasingInInnerLoops.h
  src/compiler/translator/tree_ops/ClampFragDepth.cpp
  src/compiler/translator/tree_ops/ClampFragDepth.h
  src/compiler/translator/tree_ops/ClampPointSize.cpp
  src/compiler/translator/tree_ops/ClampPointSize.h
  src/compiler/translator/tree_ops/DeclareAndInitBuiltinsForInstancedMultiview.h
  src/compiler/translator/tree_ops/DeclareAndInitBuiltinsForInstancedMultiview.cpp
  src/compiler/translator/tree_ops/DeferGlobalInitializers.cpp
  src/compiler/translator/tree_ops/DeferGlobalInitializers.h
  src/compiler/translator/tree_ops/EmulateGLDrawID.cpp
  src/compiler/translator/tree_ops/EmulateGLDrawID.h
  src/compiler/translator/tree_ops/EmulateGLFragColorBroadcast.cpp
  src/compiler/translator/tree_ops/EmulateGLFragColorBroadcast.h
  src/compiler/translator/tree_ops/EmulatePrecision.cpp
  src/compiler/translator/tree_ops/EmulatePrecision.h
  src/compiler/translator/tree_ops/ExpandIntegerPowExpressions.cpp
  src/compiler/translator/tree_ops/ExpandIntegerPowExpressions.h
  src/compiler/translator/tree_ops/FoldExpressions.cpp
  src/compiler/translator/tree_ops/FoldExpressions.h
  src/compiler/translator/tree_ops/InitializeVariables.cpp
  src/compiler/translator/tree_ops/InitializeVariables.h
  src/compiler/translator/tree_ops/NameEmbeddedUniformStructs.cpp
  src/compiler/translator/tree_ops/NameEmbeddedUniformStructs.h
  src/compiler/translator/tree_ops/PruneEmptyCases.cpp
  src/compiler/translator/tree_ops/PruneEmptyCases.h
  src/compiler/translator/tree_ops/PruneNoOps.cpp
  src/compiler/translator/tree_ops/PruneNoOps.h
  src/compiler/translator/tree_ops/RecordConstantPrecision.cpp
  src/compiler/translator/tree_ops/RecordConstantPrecision.h
  src/compiler/translator/tree_ops/RegenerateStructNames.cpp
  src/compiler/translator/tree_ops/RegenerateStructNames.h
  src/compiler/translator/tree_ops/RemoveArrayLengthMethod.cpp
  src/compiler/translator/tree_ops/RemoveArrayLengthMethod.h
  src/compiler/translator/tree_ops/RemoveInvariantDeclaration.cpp
  src/compiler/translator/tree_ops/RemoveInvariantDeclaration.h
  src/compiler/translator/tree_ops/RemovePow.cpp
  src/compiler/translator/tree_ops/RemovePow.h
  src/compiler/translator/tree_ops/RemoveUnreferencedVariables.cpp
  src/compiler/translator/tree_ops/RemoveUnreferencedVariables.h
  src/compiler/translator/tree_ops/RewriteAtomicFunctionExpressions.cpp
  src/compiler/translator/tree_ops/RewriteAtomicFunctionExpressions.h
  src/compiler/translator/tree_ops/RewriteDoWhile.cpp
  src/compiler/translator/tree_ops/RewriteDoWhile.h
  src/compiler/translator/tree_ops/RewriteExpressionsWithShaderStorageBlock.cpp
  src/compiler/translator/tree_ops/RewriteExpressionsWithShaderStorageBlock.h
  src/compiler/translator/tree_ops/RewriteStructSamplers.cpp
  src/compiler/translator/tree_ops/RewriteStructSamplers.h
  src/compiler/translator/tree_ops/RewriteRepeatedAssignToSwizzled.cpp
  src/compiler/translator/tree_ops/RewriteRepeatedAssignToSwizzled.h
  src/compiler/translator/tree_ops/RewriteTexelFetchOffset.cpp
  src/compiler/translator/tree_ops/RewriteTexelFetchOffset.h
  src/compiler/translator/tree_ops/RewriteUnaryMinusOperatorFloat.cpp
  src/compiler/translator/tree_ops/RewriteUnaryMinusOperatorFloat.h
  src/compiler/translator/tree_ops/RewriteUnaryMinusOperatorInt.cpp
  src/compiler/translator/tree_ops/RewriteUnaryMinusOperatorInt.h
  src/compiler/translator/tree_ops/ScalarizeVecAndMatConstructorArgs.cpp
  src/compiler/translator/tree_ops/ScalarizeVecAndMatConstructorArgs.h
  src/compiler/translator/tree_ops/SeparateDeclarations.cpp
  src/compiler/translator/tree_ops/SeparateDeclarations.h
  src/compiler/translator/tree_ops/SimplifyLoopConditions.cpp
  src/compiler/translator/tree_ops/SimplifyLoopConditions.h
  src/compiler/translator/tree_ops/SplitSequenceOperator.cpp
  src/compiler/translator/tree_ops/SplitSequenceOperator.h
  src/compiler/translator/tree_ops/UnfoldShortCircuitAST.cpp
  src/compiler/translator/tree_ops/UnfoldShortCircuitAST.h
  src/compiler/translator/tree_ops/UseInterfaceBlockFields.cpp
  src/compiler/translator/tree_ops/UseInterfaceBlockFields.h
  src/compiler/translator/tree_ops/VectorizeVectorScalarArithmetic.cpp
  src/compiler/translator/tree_ops/VectorizeVectorScalarArithmetic.h
  src/compiler/translator/tree_util/BuiltIn_autogen.h
  src/compiler/translator/tree_util/FindMain.cpp
  src/compiler/translator/tree_util/FindMain.h
  src/compiler/translator/tree_util/FindSymbolNode.cpp
  src/compiler/translator/tree_util/FindSymbolNode.h
  src/compiler/translator/tree_util/IntermNodePatternMatcher.cpp
  src/compiler/translator/tree_util/IntermNodePatternMatcher.h
  src/compiler/translator/tree_util/IntermNode_util.cpp
  src/compiler/translator/tree_util/IntermNode_util.h
  src/compiler/translator/tree_util/IntermTraverse.cpp
  src/compiler/translator/tree_util/IntermTraverse.h
  src/compiler/translator/tree_util/NodeSearch.h
  src/compiler/translator/tree_util/ReplaceVariable.cpp
  src/compiler/translator/tree_util/ReplaceVariable.h
  src/compiler/translator/tree_util/RunAtTheEndOfShader.cpp
  src/compiler/translator/tree_util/RunAtTheEndOfShader.h
  src/compiler/translator/tree_util/Visit.h
  src/third_party/compiler/ArrayBoundsClamper.cpp
  src/third_party/compiler/ArrayBoundsClamper.h
)

set(angle_translator_essl_sources
  src/compiler/translator/OutputESSL.cpp
  src/compiler/translator/OutputESSL.h
  src/compiler/translator/TranslatorESSL.cpp
  src/compiler/translator/TranslatorESSL.h
)

set(angle_translator_glsl_sources
  src/compiler/translator/BuiltInFunctionEmulatorGLSL.cpp
  src/compiler/translator/BuiltInFunctionEmulatorGLSL.h
  src/compiler/translator/ExtensionGLSL.cpp
  src/compiler/translator/ExtensionGLSL.h
  src/compiler/translator/OutputGLSL.cpp
  src/compiler/translator/OutputGLSL.h
  src/compiler/translator/OutputGLSLBase.cpp
  src/compiler/translator/OutputGLSLBase.h
  src/compiler/translator/TranslatorGLSL.cpp
  src/compiler/translator/TranslatorGLSL.h
  src/compiler/translator/VersionGLSL.cpp
  src/compiler/translator/VersionGLSL.h
)

set(angle_translator_hlsl_sources
  src/compiler/translator/ASTMetadataHLSL.cpp
  src/compiler/translator/ASTMetadataHLSL.h
  src/compiler/translator/AtomicCounterFunctionHLSL.cpp
  src/compiler/translator/AtomicCounterFunctionHLSL.h
  src/compiler/translator/blocklayoutHLSL.cpp
  src/compiler/translator/blocklayoutHLSL.h
  src/compiler/translator/BuiltInFunctionEmulatorHLSL.cpp
  src/compiler/translator/BuiltInFunctionEmulatorHLSL.h
  src/compiler/translator/OutputHLSL.cpp
  src/compiler/translator/OutputHLSL.h
  src/compiler/translator/ResourcesHLSL.cpp
  src/compiler/translator/ResourcesHLSL.h
  src/compiler/translator/ShaderStorageBlockFunctionHLSL.cpp
  src/compiler/translator/ShaderStorageBlockFunctionHLSL.h
  src/compiler/translator/ShaderStorageBlockOutputHLSL.cpp
  src/compiler/translator/ShaderStorageBlockOutputHLSL.h
  src/compiler/translator/StructureHLSL.cpp
  src/compiler/translator/StructureHLSL.h
  src/compiler/translator/TextureFunctionHLSL.cpp
  src/compiler/translator/TextureFunctionHLSL.h
  src/compiler/translator/ImageFunctionHLSL.cpp
  src/compiler/translator/ImageFunctionHLSL.h
  src/compiler/translator/TranslatorHLSL.cpp
  src/compiler/translator/TranslatorHLSL.h
  src/compiler/translator/UtilsHLSL.cpp
  src/compiler/translator/UtilsHLSL.h
  src/compiler/translator/emulated_builtin_functions_hlsl_autogen.cpp
  src/compiler/translator/tree_ops/AddDefaultReturnStatements.cpp
  src/compiler/translator/tree_ops/AddDefaultReturnStatements.h
  src/compiler/translator/tree_ops/ArrayReturnValueToOutParameter.cpp
  src/compiler/translator/tree_ops/ArrayReturnValueToOutParameter.h
  src/compiler/translator/tree_ops/RemoveDynamicIndexing.cpp
  src/compiler/translator/tree_ops/RemoveDynamicIndexing.h
  src/compiler/translator/tree_ops/RemoveSwitchFallThrough.cpp
  src/compiler/translator/tree_ops/RemoveSwitchFallThrough.h
  src/compiler/translator/tree_ops/RewriteElseBlocks.cpp
  src/compiler/translator/tree_ops/RewriteElseBlocks.h
  src/compiler/translator/tree_ops/SeparateArrayConstructorStatements.cpp
  src/compiler/translator/tree_ops/SeparateArrayConstructorStatements.h
  src/compiler/translator/tree_ops/SeparateArrayInitialization.cpp
  src/compiler/translator/tree_ops/SeparateArrayInitialization.h
  src/compiler/translator/tree_ops/SeparateExpressionsReturningArrays.cpp
  src/compiler/translator/tree_ops/SeparateExpressionsReturningArrays.h
  src/compiler/translator/tree_ops/UnfoldShortCircuitToIf.cpp
  src/compiler/translator/tree_ops/UnfoldShortCircuitToIf.h
  src/compiler/translator/tree_ops/WrapSwitchStatementsInBlocks.cpp
  src/compiler/translator/tree_ops/WrapSwitchStatementsInBlocks.h
)

set(angle_translator_lib_vulkan_sources
  src/compiler/translator/OutputVulkanGLSL.cpp
  src/compiler/translator/OutputVulkanGLSL.h
  src/compiler/translator/TranslatorVulkan.cpp
  src/compiler/translator/TranslatorVulkan.h
)

set(angle_preprocessor_sources
  src/compiler/preprocessor/DiagnosticsBase.cpp
  src/compiler/preprocessor/DiagnosticsBase.h
  src/compiler/preprocessor/DirectiveHandlerBase.cpp
  src/compiler/preprocessor/DirectiveHandlerBase.h
  src/compiler/preprocessor/DirectiveParser.cpp
  src/compiler/preprocessor/DirectiveParser.h
  src/compiler/preprocessor/ExpressionParser.cpp
  src/compiler/preprocessor/ExpressionParser.h
  src/compiler/preprocessor/ExpressionParser.y
  src/compiler/preprocessor/Input.cpp
  src/compiler/preprocessor/Input.h
  src/compiler/preprocessor/Lexer.cpp
  src/compiler/preprocessor/Lexer.h
  src/compiler/preprocessor/Macro.cpp
  src/compiler/preprocessor/Macro.h
  src/compiler/preprocessor/MacroExpander.cpp
  src/compiler/preprocessor/MacroExpander.h
  src/compiler/preprocessor/Preprocessor.cpp
  src/compiler/preprocessor/Preprocessor.h
  src/compiler/preprocessor/SourceLocation.h
  src/compiler/preprocessor/Token.cpp
  src/compiler/preprocessor/Token.h
  src/compiler/preprocessor/Tokenizer.cpp
  src/compiler/preprocessor/Tokenizer.h
  src/compiler/preprocessor/Tokenizer.l
  src/compiler/preprocessor/numeric_lex.h
)

set(libangle_common_sources
  src/common/Color.h
  src/common/Color.inl
  src/common/FastVector.h
  src/common/FixedVector.h
  src/common/Float16ToFloat32.cpp
  src/common/MemoryBuffer.cpp
  src/common/MemoryBuffer.h
  src/common/Optional.h
  src/common/PackedEGLEnums_autogen.cpp
  src/common/PackedEGLEnums_autogen.h
  src/common/PackedEnums.cpp
  src/common/PackedEnums.h
  src/common/PackedGLEnums_autogen.cpp
  src/common/PackedGLEnums_autogen.h
  src/common/PoolAlloc.cpp
  src/common/PoolAlloc.h
  src/common/aligned_memory.cpp
  src/common/aligned_memory.h
  src/common/angleutils.cpp
  src/common/angleutils.h
  src/common/bitset_utils.h
  src/common/debug.cpp
  src/common/debug.h
  src/common/hash_utils.h
  src/common/mathutil.cpp
  src/common/mathutil.h
  src/common/matrix_utils.cpp
  src/common/matrix_utils.h
  src/common/platform.h
  src/common/string_utils.cpp
  src/common/string_utils.h
  src/common/third_party/base/anglebase/base_export.h
  src/common/third_party/base/anglebase/containers/mru_cache.h
  src/common/third_party/base/anglebase/logging.h
  src/common/third_party/base/anglebase/macros.h
  src/common/third_party/base/anglebase/numerics/safe_conversions.h
  src/common/third_party/base/anglebase/numerics/safe_conversions_impl.h
  src/common/third_party/base/anglebase/numerics/safe_math.h
  src/common/third_party/base/anglebase/numerics/safe_math_impl.h
  src/common/third_party/base/anglebase/sha1.cc
  src/common/third_party/base/anglebase/sha1.h
  src/common/third_party/base/anglebase/sys_byteorder.h
  src/common/third_party/smhasher/src/PMurHash.cpp
  src/common/third_party/smhasher/src/PMurHash.h
  src/common/tls.cpp
  src/common/tls.h
  src/common/uniform_type_info_autogen.cpp
  src/common/utilities.cpp
  src/common/utilities.h
  src/common/vector_utils.h
)

set(xxhash_sources
  src/common/third_party/xxhash/xxhash.c
  src/common/third_party/xxhash/xxhash.h
)

set(angle_system_utils_sources
  src/common/Optional.h
  src/common/angleutils.h
  src/common/platform.h
  src/common/system_utils.cpp
  src/common/system_utils.h
)

if(UNIX)
  list(APPEND angle_system_utils_sources
    src/common/system_utils_linux.cpp
    src/common/system_utils_posix.cpp
  )
endif()

if(APPLE)
  list(APPEND angle_system_utils_sources
    src/common/system_utils_mac.cpp
    src/common/system_utils_posix.cpp
  )
endif()

if(WIN32)
  list(APPEND angle_system_utils_sources
    src/common/system_utils_win.cpp
  )
endif()

if(ANDROID)
  list(APPEND angle_system_utils_sources
    src/common/android_util.cpp
    src/common/android_util.h
  )
endif()

set(libangle_image_util_sources
  src/image_util/copyimage.cpp
  src/image_util/copyimage.h
  src/image_util/copyimage.inl
  src/image_util/generatemip.h
  src/image_util/generatemip.inl
  src/image_util/imageformats.cpp
  src/image_util/imageformats.h
  src/image_util/loadimage.cpp
  src/image_util/loadimage.h
  src/image_util/loadimage.inl
  src/image_util/loadimage_etc.cpp
)

set(libangle_gpu_info_util_sources
  src/gpu_info_util/SystemInfo.cpp
  src/gpu_info_util/SystemInfo.h
  src/gpu_info_util/SystemInfo_internal.h
)

set(libangle_gpu_info_util_win_sources src/gpu_info_util/SystemInfo_win.cpp)
set(libangle_gpu_info_util_linux_sources src/gpu_info_util/SystemInfo_linux.cpp)
set(libangle_gpu_info_util_libpci_sources src/gpu_info_util/SystemInfo_libpci.cpp)
set(libangle_gpu_info_util_x11_sources src/gpu_info_util/SystemInfo_x11.cpp)
set(libangle_gpu_info_util_mac_sources src/gpu_info_util/SystemInfo_mac.mm)

set(libangle_includes
  include/angle_gl.h
  include/export.h
  include/EGL/egl.h
  include/EGL/eglext.h
  include/EGL/eglext_angle.h
  include/EGL/eglplatform.h
  include/GLES/gl.h
  include/GLES/glplatform.h
  include/GLES/glext.h
  include/GLES/glext_angle.h
  include/GLES/glext_explicit_context_autogen.inc
  include/GLES2/gl2.h
  include/GLES2/gl2ext.h
  include/GLES2/gl2ext_angle.h
  include/GLES2/gl2ext_explicit_context_autogen.inc
  include/GLES2/gl2platform.h
  include/GLES3/gl3.h
  include/GLES3/gl3ext_explicit_context_autogen.inc
  include/GLES3/gl3platform.h
  include/GLES3/gl31.h
  include/GLES3/gl31ext_explicit_context_autogen.inc
  include/GLES3/gl32.h
  include/GLSLANG/ShaderLang.h
  include/GLSLANG/ShaderVars.h
  include/KHR/khrplatform.h
  include/WGL/wgl.h
  include/platform/FeaturesVk.h
  include/platform/Platform.h
  include/platform/WorkaroundsD3D.h
)

set(libangle_sources
  src/common/event_tracer.cpp
  src/common/event_tracer.h
  src/libANGLE/AttributeMap.cpp
  src/libANGLE/AttributeMap.h
  src/libANGLE/BinaryStream.h
  src/libANGLE/BlobCache.cpp
  src/libANGLE/BlobCache.h
  src/libANGLE/Buffer.cpp
  src/libANGLE/Buffer.h
  src/libANGLE/Caps.cpp
  src/libANGLE/Caps.h
  src/libANGLE/Compiler.cpp
  src/libANGLE/Compiler.h
  src/libANGLE/Config.cpp
  src/libANGLE/Config.h
  src/libANGLE/Constants.h
  src/libANGLE/Context.cpp
  src/libANGLE/Context_gles_1_0.cpp
  src/libANGLE/Context_gles_1_0_autogen.h
  src/libANGLE/Context.h
  src/libANGLE/Debug.cpp
  src/libANGLE/Debug.h
  src/libANGLE/Device.cpp
  src/libANGLE/Device.h
  src/libANGLE/Display.cpp
  src/libANGLE/Display.h
  src/libANGLE/EGLSync.cpp
  src/libANGLE/EGLSync.h
  src/libANGLE/Error.cpp
  src/libANGLE/Error.h
  src/libANGLE/Error.inl
  src/libANGLE/ErrorStrings.h
  src/libANGLE/Fence.cpp
  src/libANGLE/Fence.h
  src/libANGLE/Framebuffer.cpp
  src/libANGLE/Framebuffer.h
  src/libANGLE/FramebufferAttachment.cpp
  src/libANGLE/FramebufferAttachment.h
  src/libANGLE/GLES1Renderer.cpp
  src/libANGLE/GLES1Renderer.h
  src/libANGLE/GLES1Shaders.inc
  src/libANGLE/GLES1State.cpp
  src/libANGLE/GLES1State.h
  src/libANGLE/HandleAllocator.cpp
  src/libANGLE/HandleAllocator.h
  src/libANGLE/HandleRangeAllocator.h
  src/libANGLE/HandleRangeAllocator.cpp
  src/libANGLE/Image.h
  src/libANGLE/Image.cpp
  src/libANGLE/ImageIndex.h
  src/libANGLE/ImageIndex.cpp
  src/libANGLE/IndexRangeCache.cpp
  src/libANGLE/IndexRangeCache.h
  src/libANGLE/LoggingAnnotator.cpp
  src/libANGLE/LoggingAnnotator.h
  src/libANGLE/MemoryObject.cpp
  src/libANGLE/MemoryObject.h
  src/libANGLE/MemoryProgramCache.cpp
  src/libANGLE/MemoryProgramCache.h
  src/libANGLE/Observer.cpp
  src/libANGLE/Observer.h
  src/libANGLE/Path.h
  src/libANGLE/Path.cpp
  src/libANGLE/Platform.cpp
  src/libANGLE/Program.cpp
  src/libANGLE/Program.h
  src/libANGLE/ProgramLinkedResources.cpp
  src/libANGLE/ProgramLinkedResources.h
  src/libANGLE/ProgramPipeline.cpp
  src/libANGLE/ProgramPipeline.h
  src/libANGLE/Query.cpp
  src/libANGLE/Query.h
  src/libANGLE/RefCountObject.h
  src/libANGLE/Renderbuffer.cpp
  src/libANGLE/Renderbuffer.h
  src/libANGLE/ResourceManager.cpp
  src/libANGLE/ResourceManager.h
  src/libANGLE/ResourceMap.h
  src/libANGLE/Sampler.cpp
  src/libANGLE/Sampler.h
  src/libANGLE/Shader.cpp
  src/libANGLE/Shader.h
  src/libANGLE/SizedMRUCache.h
  src/libANGLE/State.cpp
  src/libANGLE/State.h
  src/libANGLE/Stream.cpp
  src/libANGLE/Stream.h
  src/libANGLE/Surface.cpp
  src/libANGLE/Surface.h
  src/libANGLE/Texture.cpp
  src/libANGLE/Texture.h
  src/libANGLE/Thread.cpp
  src/libANGLE/Thread.h
  src/libANGLE/TransformFeedback.cpp
  src/libANGLE/TransformFeedback.h
  src/libANGLE/Uniform.cpp
  src/libANGLE/Uniform.h
  src/libANGLE/VaryingPacking.cpp
  src/libANGLE/VaryingPacking.h
  src/libANGLE/Version.h
  src/libANGLE/Version.inl
  src/libANGLE/VertexArray.cpp
  src/libANGLE/VertexArray.h
  src/libANGLE/VertexAttribute.cpp
  src/libANGLE/VertexAttribute.h
  src/libANGLE/VertexAttribute.inl
  src/libANGLE/Workarounds.h
  src/libANGLE/WorkerThread.cpp
  src/libANGLE/WorkerThread.h
  src/libANGLE/angletypes.cpp
  src/libANGLE/angletypes.h
  src/libANGLE/angletypes.inl
  src/libANGLE/es3_copy_conversion_table_autogen.cpp
  src/libANGLE/features.h
  src/libANGLE/format_map_autogen.cpp
  src/libANGLE/formatutils.cpp
  src/libANGLE/formatutils.h
  src/libANGLE/histogram_macros.h
  src/libANGLE/queryconversions.cpp
  src/libANGLE/queryconversions.h
  src/libANGLE/queryutils.cpp
  src/libANGLE/queryutils.h
  src/libANGLE/renderer/BufferImpl.h
  src/libANGLE/renderer/CompilerImpl.h
  src/libANGLE/renderer/ContextImpl.cpp
  src/libANGLE/renderer/ContextImpl.h
  src/libANGLE/renderer/driver_utils.cpp
  src/libANGLE/renderer/driver_utils.h
  src/libANGLE/renderer/DeviceImpl.cpp
  src/libANGLE/renderer/DeviceImpl.h
  src/libANGLE/renderer/DisplayImpl.cpp
  src/libANGLE/renderer/DisplayImpl.h
  src/libANGLE/renderer/EGLImplFactory.h
  src/libANGLE/renderer/EGLSyncImpl.h
  src/libANGLE/renderer/FenceNVImpl.h
  src/libANGLE/renderer/FormatID_autogen.h
  src/libANGLE/renderer/Format_table_autogen.cpp
  src/libANGLE/renderer/Format.h
  src/libANGLE/renderer/FramebufferAttachmentObjectImpl.h
  src/libANGLE/renderer/FramebufferImpl.h
  src/libANGLE/renderer/GLImplFactory.h
  src/libANGLE/renderer/ImageImpl.h
  src/libANGLE/renderer/PathImpl.h
  src/libANGLE/renderer/ProgramImpl.h
  src/libANGLE/renderer/ProgramPipelineImpl.h
  src/libANGLE/renderer/QueryImpl.cpp
  src/libANGLE/renderer/QueryImpl.h
  src/libANGLE/renderer/RenderbufferImpl.h
  src/libANGLE/renderer/RenderTargetCache.h
  src/libANGLE/renderer/SamplerImpl.h
  src/libANGLE/renderer/ShaderImpl.cpp
  src/libANGLE/renderer/ShaderImpl.h
  src/libANGLE/renderer/StreamProducerImpl.h
  src/libANGLE/renderer/SurfaceImpl.cpp
  src/libANGLE/renderer/SurfaceImpl.h
  src/libANGLE/renderer/SyncImpl.h
  src/libANGLE/renderer/TextureImpl.cpp
  src/libANGLE/renderer/TextureImpl.h
  src/libANGLE/renderer/TransformFeedbackImpl.h
  src/libANGLE/renderer/VertexArrayImpl.h
  src/libANGLE/renderer/copyvertex.h
  src/libANGLE/renderer/copyvertex.inc
  src/libANGLE/renderer/load_functions_table.h
  src/libANGLE/renderer/load_functions_table_autogen.cpp
  src/libANGLE/renderer/renderer_utils.cpp
  src/libANGLE/renderer/renderer_utils.h
  src/libANGLE/validationEGL.cpp
  src/libANGLE/validationEGL.h
  src/libANGLE/validationES.cpp
  src/libANGLE/validationES.h
  src/libANGLE/validationES1.cpp
  src/libANGLE/validationES1_autogen.h
  src/libANGLE/validationES1.h
  src/libANGLE/validationES2.cpp
  src/libANGLE/validationES2_autogen.h
  src/libANGLE/validationES2.h
  src/libANGLE/validationES3.cpp
  src/libANGLE/validationES31.cpp
  src/libANGLE/validationES31_autogen.h
  src/libANGLE/validationES31.h
  src/libANGLE/validationES3_autogen.h
  src/libANGLE/validationES3.h
  src/libANGLE/validationESEXT_autogen.h
  src/libANGLE/validationESEXT.h
  src/third_party/trace_event/trace_event.h
)

set(libangle_d3d_shared_sources
  src/libANGLE/renderer/d3d/BufferD3D.cpp
  src/libANGLE/renderer/d3d/BufferD3D.h
  src/libANGLE/renderer/d3d/CompilerD3D.cpp
  src/libANGLE/renderer/d3d/CompilerD3D.h
  src/libANGLE/renderer/d3d/ContextD3D.h
  src/libANGLE/renderer/d3d/DeviceD3D.cpp
  src/libANGLE/renderer/d3d/DeviceD3D.h
  src/libANGLE/renderer/d3d/DisplayD3D.cpp
  src/libANGLE/renderer/d3d/DisplayD3D.h
  src/libANGLE/renderer/d3d/DynamicHLSL.cpp
  src/libANGLE/renderer/d3d/DynamicHLSL.h
  src/libANGLE/renderer/d3d/DynamicImage2DHLSL.cpp
  src/libANGLE/renderer/d3d/DynamicImage2DHLSL.h
  src/libANGLE/renderer/d3d/EGLImageD3D.cpp
  src/libANGLE/renderer/d3d/EGLImageD3D.h
  src/libANGLE/renderer/d3d/formatutilsD3D.h
  src/libANGLE/renderer/d3d/FramebufferD3D.cpp
  src/libANGLE/renderer/d3d/FramebufferD3D.h
  src/libANGLE/renderer/d3d/HLSLCompiler.cpp
  src/libANGLE/renderer/d3d/HLSLCompiler.h
  src/libANGLE/renderer/d3d/ImageD3D.cpp
  src/libANGLE/renderer/d3d/ImageD3D.h
  src/libANGLE/renderer/d3d/IndexBuffer.cpp
  src/libANGLE/renderer/d3d/IndexBuffer.h
  src/libANGLE/renderer/d3d/IndexDataManager.cpp
  src/libANGLE/renderer/d3d/IndexDataManager.h
  src/libANGLE/renderer/d3d/NativeWindowD3D.cpp
  src/libANGLE/renderer/d3d/NativeWindowD3D.h
  src/libANGLE/renderer/d3d/ProgramD3D.cpp
  src/libANGLE/renderer/d3d/ProgramD3D.h
  src/libANGLE/renderer/d3d/RenderbufferD3D.cpp
  src/libANGLE/renderer/d3d/RenderbufferD3D.h
  src/libANGLE/renderer/d3d/RendererD3D.cpp
  src/libANGLE/renderer/d3d/RendererD3D.h
  src/libANGLE/renderer/d3d/RenderTargetD3D.h
  src/libANGLE/renderer/d3d/RenderTargetD3D.cpp
  src/libANGLE/renderer/d3d/SamplerD3D.h
  src/libANGLE/renderer/d3d/ShaderD3D.cpp
  src/libANGLE/renderer/d3d/ShaderD3D.h
  src/libANGLE/renderer/d3d/ShaderExecutableD3D.cpp
  src/libANGLE/renderer/d3d/ShaderExecutableD3D.h
  src/libANGLE/renderer/d3d/SurfaceD3D.cpp
  src/libANGLE/renderer/d3d/SurfaceD3D.h
  src/libANGLE/renderer/d3d/SwapChainD3D.cpp
  src/libANGLE/renderer/d3d/SwapChainD3D.h
  src/libANGLE/renderer/d3d/TextureD3D.cpp
  src/libANGLE/renderer/d3d/TextureD3D.h
  src/libANGLE/renderer/d3d/TextureStorage.h
  src/libANGLE/renderer/d3d/VertexBuffer.cpp
  src/libANGLE/renderer/d3d/VertexBuffer.h
  src/libANGLE/renderer/d3d/VertexDataManager.cpp
  src/libANGLE/renderer/d3d/VertexDataManager.h
)

set(libangle_d3d9_sources
  src/libANGLE/renderer/d3d/d3d9/Blit9.cpp
  src/libANGLE/renderer/d3d/d3d9/Blit9.h
  src/libANGLE/renderer/d3d/d3d9/Buffer9.cpp
  src/libANGLE/renderer/d3d/d3d9/Buffer9.h
  src/libANGLE/renderer/d3d/d3d9/Context9.cpp
  src/libANGLE/renderer/d3d/d3d9/Context9.h
  src/libANGLE/renderer/d3d/d3d9/DebugAnnotator9.cpp
  src/libANGLE/renderer/d3d/d3d9/DebugAnnotator9.h
  src/libANGLE/renderer/d3d/d3d9/Fence9.cpp
  src/libANGLE/renderer/d3d/d3d9/Fence9.h
  src/libANGLE/renderer/d3d/d3d9/formatutils9.cpp
  src/libANGLE/renderer/d3d/d3d9/formatutils9.h
  src/libANGLE/renderer/d3d/d3d9/Framebuffer9.cpp
  src/libANGLE/renderer/d3d/d3d9/Framebuffer9.h
  src/libANGLE/renderer/d3d/d3d9/Image9.cpp
  src/libANGLE/renderer/d3d/d3d9/Image9.h
  src/libANGLE/renderer/d3d/d3d9/IndexBuffer9.cpp
  src/libANGLE/renderer/d3d/d3d9/IndexBuffer9.h
  src/libANGLE/renderer/d3d/d3d9/NativeWindow9.cpp
  src/libANGLE/renderer/d3d/d3d9/NativeWindow9.h
  src/libANGLE/renderer/d3d/d3d9/Query9.cpp
  src/libANGLE/renderer/d3d/d3d9/Query9.h
  src/libANGLE/renderer/d3d/d3d9/Renderer9.cpp
  src/libANGLE/renderer/d3d/d3d9/Renderer9.h
  src/libANGLE/renderer/d3d/d3d9/renderer9_utils.cpp
  src/libANGLE/renderer/d3d/d3d9/renderer9_utils.h
  src/libANGLE/renderer/d3d/d3d9/RenderTarget9.cpp
  src/libANGLE/renderer/d3d/d3d9/RenderTarget9.h
  src/libANGLE/renderer/d3d/d3d9/ShaderCache.h
  src/libANGLE/renderer/d3d/d3d9/ShaderExecutable9.cpp
  src/libANGLE/renderer/d3d/d3d9/ShaderExecutable9.h
  src/libANGLE/renderer/d3d/d3d9/shaders/compiled/componentmaskps.h
  src/libANGLE/renderer/d3d/d3d9/shaders/compiled/componentmaskpremultps.h
  src/libANGLE/renderer/d3d/d3d9/shaders/compiled/componentmaskunmultps.h
  src/libANGLE/renderer/d3d/d3d9/shaders/compiled/luminanceps.h
  src/libANGLE/renderer/d3d/d3d9/shaders/compiled/luminancepremultps.h
  src/libANGLE/renderer/d3d/d3d9/shaders/compiled/luminanceunmultps.h
  src/libANGLE/renderer/d3d/d3d9/shaders/compiled/passthroughps.h
  src/libANGLE/renderer/d3d/d3d9/shaders/compiled/standardvs.h
  src/libANGLE/renderer/d3d/d3d9/StateManager9.cpp
  src/libANGLE/renderer/d3d/d3d9/StateManager9.h
  src/libANGLE/renderer/d3d/d3d9/SwapChain9.cpp
  src/libANGLE/renderer/d3d/d3d9/SwapChain9.h
  src/libANGLE/renderer/d3d/d3d9/TextureStorage9.cpp
  src/libANGLE/renderer/d3d/d3d9/TextureStorage9.h
  src/libANGLE/renderer/d3d/d3d9/VertexArray9.h
  src/libANGLE/renderer/d3d/d3d9/VertexBuffer9.cpp
  src/libANGLE/renderer/d3d/d3d9/VertexBuffer9.h
  src/libANGLE/renderer/d3d/d3d9/vertexconversion.h
  src/libANGLE/renderer/d3d/d3d9/VertexDeclarationCache.cpp
  src/libANGLE/renderer/d3d/d3d9/VertexDeclarationCache.h
)

set(libangle_d3d11_sources
  src/libANGLE/renderer/d3d/d3d11/Blit11.cpp
  src/libANGLE/renderer/d3d/d3d11/Blit11.h
  src/libANGLE/renderer/d3d/d3d11/Blit11Helper_autogen.inc
  src/libANGLE/renderer/d3d/d3d11/Buffer11.cpp
  src/libANGLE/renderer/d3d/d3d11/Buffer11.h
  src/libANGLE/renderer/d3d/d3d11/Clear11.cpp
  src/libANGLE/renderer/d3d/d3d11/Clear11.h
  src/libANGLE/renderer/d3d/d3d11/Context11.cpp
  src/libANGLE/renderer/d3d/d3d11/Context11.h
  src/libANGLE/renderer/d3d/d3d11/DebugAnnotator11.cpp
  src/libANGLE/renderer/d3d/d3d11/DebugAnnotator11.h
  src/libANGLE/renderer/d3d/d3d11/dxgi_format_map_autogen.cpp
  src/libANGLE/renderer/d3d/d3d11/dxgi_support_table_autogen.cpp
  src/libANGLE/renderer/d3d/d3d11/dxgi_support_table.h
  src/libANGLE/renderer/d3d/d3d11/Fence11.cpp
  src/libANGLE/renderer/d3d/d3d11/Fence11.h
  src/libANGLE/renderer/d3d/d3d11/formatutils11.cpp
  src/libANGLE/renderer/d3d/d3d11/formatutils11.h
  src/libANGLE/renderer/d3d/d3d11/Framebuffer11.cpp
  src/libANGLE/renderer/d3d/d3d11/Framebuffer11.h
  src/libANGLE/renderer/d3d/d3d11/Image11.cpp
  src/libANGLE/renderer/d3d/d3d11/Image11.h
  src/libANGLE/renderer/d3d/d3d11/IndexBuffer11.cpp
  src/libANGLE/renderer/d3d/d3d11/IndexBuffer11.h
  src/libANGLE/renderer/d3d/d3d11/InputLayoutCache.cpp
  src/libANGLE/renderer/d3d/d3d11/InputLayoutCache.h
  src/libANGLE/renderer/d3d/d3d11/NativeWindow11.h
  src/libANGLE/renderer/d3d/d3d11/PixelTransfer11.cpp
  src/libANGLE/renderer/d3d/d3d11/PixelTransfer11.h
  src/libANGLE/renderer/d3d/d3d11/Program11.cpp
  src/libANGLE/renderer/d3d/d3d11/Program11.h
  src/libANGLE/renderer/d3d/d3d11/ProgramPipeline11.cpp
  src/libANGLE/renderer/d3d/d3d11/ProgramPipeline11.h
  src/libANGLE/renderer/d3d/d3d11/Query11.cpp
  src/libANGLE/renderer/d3d/d3d11/Query11.h
  src/libANGLE/renderer/d3d/d3d11/Renderer11.cpp
  src/libANGLE/renderer/d3d/d3d11/Renderer11.h
  src/libANGLE/renderer/d3d/d3d11/renderer11_utils.cpp
  src/libANGLE/renderer/d3d/d3d11/renderer11_utils.h
  src/libANGLE/renderer/d3d/d3d11/RenderStateCache.cpp
  src/libANGLE/renderer/d3d/d3d11/RenderStateCache.h
  src/libANGLE/renderer/d3d/d3d11/RenderTarget11.cpp
  src/libANGLE/renderer/d3d/d3d11/RenderTarget11.h
  src/libANGLE/renderer/d3d/d3d11/ResourceManager11.cpp
  src/libANGLE/renderer/d3d/d3d11/ResourceManager11.h
  src/libANGLE/renderer/d3d/d3d11/ShaderExecutable11.cpp
  src/libANGLE/renderer/d3d/d3d11/ShaderExecutable11.h
  src/libANGLE/renderer/d3d/d3d11/shaders/compiled/buffertotexture11_gs.h
  src/libANGLE/renderer/d3d/d3d11/shaders/compiled/buffertotexture11_ps_4f.h
  src/libANGLE/renderer/d3d/d3d11/shaders/compiled/buffertotexture11_ps_4i.h
  src/libANGLE/renderer/d3d/d3d11/shaders/compiled/buffertotexture11_ps_4ui.h
  src/libANGLE/renderer/d3d/d3d11/shaders/compiled/buffertotexture11_vs.h
  src/libANGLE/renderer/d3d/d3d11/shaders/compiled/clear11_fl9vs.h
  src/libANGLE/renderer/d3d/d3d11/shaders/compiled/clear11multiviewgs.h
  src/libANGLE/renderer/d3d/d3d11/shaders/compiled/clear11multiviewvs.h
  src/libANGLE/renderer/d3d/d3d11/shaders/compiled/clear11vs.h
  src/libANGLE/renderer/d3d/d3d11/shaders/compiled/cleardepth11ps.h
  src/libANGLE/renderer/d3d/d3d11/shaders/compiled/clearfloat11_fl9ps.h
  src/libANGLE/renderer/d3d/d3d11/shaders/compiled/clearfloat11ps1.h
  src/libANGLE/renderer/d3d/d3d11/shaders/compiled/clearfloat11ps2.h
  src/libANGLE/renderer/d3d/d3d11/shaders/compiled/clearfloat11ps3.h
  src/libANGLE/renderer/d3d/d3d11/shaders/compiled/clearfloat11ps4.h
  src/libANGLE/renderer/d3d/d3d11/shaders/compiled/clearfloat11ps5.h
  src/libANGLE/renderer/d3d/d3d11/shaders/compiled/clearfloat11ps6.h
  src/libANGLE/renderer/d3d/d3d11/shaders/compiled/clearfloat11ps7.h
  src/libANGLE/renderer/d3d/d3d11/shaders/compiled/clearfloat11ps8.h
  src/libANGLE/renderer/d3d/d3d11/shaders/compiled/clearsint11ps1.h
  src/libANGLE/renderer/d3d/d3d11/shaders/compiled/clearsint11ps2.h
  src/libANGLE/renderer/d3d/d3d11/shaders/compiled/clearsint11ps3.h
  src/libANGLE/renderer/d3d/d3d11/shaders/compiled/clearsint11ps4.h
  src/libANGLE/renderer/d3d/d3d11/shaders/compiled/clearsint11ps5.h
  src/libANGLE/renderer/d3d/d3d11/shaders/compiled/clearsint11ps6.h
  src/libANGLE/renderer/d3d/d3d11/shaders/compiled/clearsint11ps7.h
  src/libANGLE/renderer/d3d/d3d11/shaders/compiled/clearsint11ps8.h
  src/libANGLE/renderer/d3d/d3d11/shaders/compiled/clearuint11ps1.h
  src/libANGLE/renderer/d3d/d3d11/shaders/compiled/clearuint11ps2.h
  src/libANGLE/renderer/d3d/d3d11/shaders/compiled/clearuint11ps3.h
  src/libANGLE/renderer/d3d/d3d11/shaders/compiled/clearuint11ps4.h
  src/libANGLE/renderer/d3d/d3d11/shaders/compiled/clearuint11ps5.h
  src/libANGLE/renderer/d3d/d3d11/shaders/compiled/clearuint11ps6.h
  src/libANGLE/renderer/d3d/d3d11/shaders/compiled/clearuint11ps7.h
  src/libANGLE/renderer/d3d/d3d11/shaders/compiled/clearuint11ps8.h
  src/libANGLE/renderer/d3d/d3d11/shaders/compiled/passthrough2d11vs.h
  src/libANGLE/renderer/d3d/d3d11/shaders/compiled/passthrough3d11gs.h
  src/libANGLE/renderer/d3d/d3d11/shaders/compiled/passthrough3d11vs.h
  src/libANGLE/renderer/d3d/d3d11/shaders/compiled/passthroughdepth2d11ps.h
  src/libANGLE/renderer/d3d/d3d11/shaders/compiled/resolvecolor2dps.h
  src/libANGLE/renderer/d3d/d3d11/shaders/compiled/resolvedepth11_ps.h
  src/libANGLE/renderer/d3d/d3d11/shaders/compiled/resolvedepthstencil11_ps.h
  src/libANGLE/renderer/d3d/d3d11/shaders/compiled/resolvedepthstencil11_vs.h
  src/libANGLE/renderer/d3d/d3d11/shaders/compiled/resolvestencil11_ps.h
  src/libANGLE/renderer/d3d/d3d11/shaders/compiled/swizzlef2darrayps.h
  src/libANGLE/renderer/d3d/d3d11/shaders/compiled/swizzlef2dps.h
  src/libANGLE/renderer/d3d/d3d11/shaders/compiled/swizzlef3dps.h
  src/libANGLE/renderer/d3d/d3d11/shaders/compiled/swizzlei2darrayps.h
  src/libANGLE/renderer/d3d/d3d11/shaders/compiled/swizzlei2dps.h
  src/libANGLE/renderer/d3d/d3d11/shaders/compiled/swizzlei3dps.h
  src/libANGLE/renderer/d3d/d3d11/shaders/compiled/swizzleui2darrayps.h
  src/libANGLE/renderer/d3d/d3d11/shaders/compiled/swizzleui2dps.h
  src/libANGLE/renderer/d3d/d3d11/shaders/compiled/swizzleui3dps.h
  src/libANGLE/renderer/d3d/d3d11/StateManager11.cpp
  src/libANGLE/renderer/d3d/d3d11/StateManager11.h
  src/libANGLE/renderer/d3d/d3d11/StreamProducerD3DTexture.cpp
  src/libANGLE/renderer/d3d/d3d11/StreamProducerD3DTexture.h
  src/libANGLE/renderer/d3d/d3d11/SwapChain11.cpp
  src/libANGLE/renderer/d3d/d3d11/SwapChain11.h
  src/libANGLE/renderer/d3d/d3d11/texture_format_table.cpp
  src/libANGLE/renderer/d3d/d3d11/texture_format_table.h
  src/libANGLE/renderer/d3d/d3d11/texture_format_table_autogen.cpp
  src/libANGLE/renderer/d3d/d3d11/texture_format_table_utils.h
  src/libANGLE/renderer/d3d/d3d11/TextureStorage11.cpp
  src/libANGLE/renderer/d3d/d3d11/TextureStorage11.h
  src/libANGLE/renderer/d3d/d3d11/TransformFeedback11.cpp
  src/libANGLE/renderer/d3d/d3d11/TransformFeedback11.h
  src/libANGLE/renderer/d3d/d3d11/Trim11.cpp
  src/libANGLE/renderer/d3d/d3d11/Trim11.h
  src/libANGLE/renderer/d3d/d3d11/VertexArray11.cpp
  src/libANGLE/renderer/d3d/d3d11/VertexArray11.h
  src/libANGLE/renderer/d3d/d3d11/VertexBuffer11.cpp
  src/libANGLE/renderer/d3d/d3d11/VertexBuffer11.h
)

set(libangle_d3d11_win32_sources
  src/libANGLE/renderer/d3d/d3d11/win32/NativeWindow11Win32.cpp
  src/libANGLE/renderer/d3d/d3d11/win32/NativeWindow11Win32.h
  src/libANGLE/renderer/d3d/d3d11/converged/CompositorNativeWindow11.cpp
  src/libANGLE/renderer/d3d/d3d11/converged/CompositorNativeWindow11.h
  src/third_party/systeminfo/SystemInfo.cpp
  src/third_party/systeminfo/SystemInfo.h
)

set(libangle_d3d11_winrt_sources
  src/libANGLE/renderer/d3d/d3d11/winrt/CoreWindowNativeWindow.cpp
  src/libANGLE/renderer/d3d/d3d11/winrt/CoreWindowNativeWindow.h
  src/libANGLE/renderer/d3d/d3d11/winrt/InspectableNativeWindow.cpp
  src/libANGLE/renderer/d3d/d3d11/winrt/InspectableNativeWindow.h
  src/libANGLE/renderer/d3d/d3d11/winrt/NativeWindow11WinRT.cpp
  src/libANGLE/renderer/d3d/d3d11/winrt/NativeWindow11WinRT.h
  src/libANGLE/renderer/d3d/d3d11/winrt/SwapChainPanelNativeWindow.cpp
  src/libANGLE/renderer/d3d/d3d11/winrt/SwapChainPanelNativeWindow.h
)

set(libangle_gl_sources
  src/libANGLE/renderer/gl/BlitGL.cpp
  src/libANGLE/renderer/gl/BlitGL.h
  src/libANGLE/renderer/gl/BufferGL.cpp
  src/libANGLE/renderer/gl/BufferGL.h
  src/libANGLE/renderer/gl/ClearMultiviewGL.cpp
  src/libANGLE/renderer/gl/ClearMultiviewGL.h
  src/libANGLE/renderer/gl/CompilerGL.cpp
  src/libANGLE/renderer/gl/CompilerGL.h
  src/libANGLE/renderer/gl/ContextGL.cpp
  src/libANGLE/renderer/gl/ContextGL.h
  src/libANGLE/renderer/gl/DispatchTableGL_autogen.cpp
  src/libANGLE/renderer/gl/DispatchTableGL_autogen.h
  src/libANGLE/renderer/gl/DisplayGL.cpp
  src/libANGLE/renderer/gl/DisplayGL.h
  src/libANGLE/renderer/gl/FenceNVGL.cpp
  src/libANGLE/renderer/gl/FenceNVGL.h
  src/libANGLE/renderer/gl/FramebufferGL.cpp
  src/libANGLE/renderer/gl/FramebufferGL.h
  src/libANGLE/renderer/gl/FunctionsGL.cpp
  src/libANGLE/renderer/gl/FunctionsGL.h
  src/libANGLE/renderer/gl/ImageGL.cpp
  src/libANGLE/renderer/gl/ImageGL.h
  src/libANGLE/renderer/gl/PathGL.h
  src/libANGLE/renderer/gl/PathGL.cpp
  src/libANGLE/renderer/gl/ProgramGL.cpp
  src/libANGLE/renderer/gl/ProgramGL.h
  src/libANGLE/renderer/gl/ProgramPipelineGL.cpp
  src/libANGLE/renderer/gl/ProgramPipelineGL.h
  src/libANGLE/renderer/gl/QueryGL.cpp
  src/libANGLE/renderer/gl/QueryGL.h
  src/libANGLE/renderer/gl/RenderbufferGL.cpp
  src/libANGLE/renderer/gl/RenderbufferGL.h
  src/libANGLE/renderer/gl/RendererGL.cpp
  src/libANGLE/renderer/gl/RendererGL.h
  src/libANGLE/renderer/gl/SamplerGL.cpp
  src/libANGLE/renderer/gl/SamplerGL.h
  src/libANGLE/renderer/gl/ShaderGL.cpp
  src/libANGLE/renderer/gl/ShaderGL.h
  src/libANGLE/renderer/gl/StateManagerGL.cpp
  src/libANGLE/renderer/gl/StateManagerGL.h
  src/libANGLE/renderer/gl/SurfaceGL.cpp
  src/libANGLE/renderer/gl/SurfaceGL.h
  src/libANGLE/renderer/gl/SyncGL.cpp
  src/libANGLE/renderer/gl/SyncGL.h
  src/libANGLE/renderer/gl/TextureGL.cpp
  src/libANGLE/renderer/gl/TextureGL.h
  src/libANGLE/renderer/gl/TransformFeedbackGL.cpp
  src/libANGLE/renderer/gl/TransformFeedbackGL.h
  src/libANGLE/renderer/gl/VertexArrayGL.cpp
  src/libANGLE/renderer/gl/VertexArrayGL.h
  src/libANGLE/renderer/gl/WorkaroundsGL.h
  src/libANGLE/renderer/gl/formatutilsgl.cpp
  src/libANGLE/renderer/gl/formatutilsgl.h
  src/libANGLE/renderer/gl/functionsgl_enums.h
  src/libANGLE/renderer/gl/functionsgl_typedefs.h
  src/libANGLE/renderer/gl/renderergl_utils.cpp
  src/libANGLE/renderer/gl/renderergl_utils.h
)

set(libangle_gl_null_sources
  src/libANGLE/renderer/gl/null_functions.cpp
  src/libANGLE/renderer/gl/null_functions.h
)

set(libangle_gl_wgl_sources
  src/libANGLE/renderer/gl/wgl/ContextWGL.cpp
  src/libANGLE/renderer/gl/wgl/ContextWGL.h
  src/libANGLE/renderer/gl/wgl/D3DTextureSurfaceWGL.cpp
  src/libANGLE/renderer/gl/wgl/D3DTextureSurfaceWGL.h
  src/libANGLE/renderer/gl/wgl/DisplayWGL.cpp
  src/libANGLE/renderer/gl/wgl/DisplayWGL.h
  src/libANGLE/renderer/gl/wgl/DXGISwapChainWindowSurfaceWGL.cpp
  src/libANGLE/renderer/gl/wgl/DXGISwapChainWindowSurfaceWGL.h
  src/libANGLE/renderer/gl/wgl/FunctionsWGL.cpp
  src/libANGLE/renderer/gl/wgl/FunctionsWGL.h
  src/libANGLE/renderer/gl/wgl/PbufferSurfaceWGL.cpp
  src/libANGLE/renderer/gl/wgl/PbufferSurfaceWGL.h
  src/libANGLE/renderer/gl/wgl/RendererWGL.cpp
  src/libANGLE/renderer/gl/wgl/RendererWGL.h
  src/libANGLE/renderer/gl/wgl/SurfaceWGL.h
  src/libANGLE/renderer/gl/wgl/WindowSurfaceWGL.cpp
  src/libANGLE/renderer/gl/wgl/WindowSurfaceWGL.h
  src/libANGLE/renderer/gl/wgl/functionswgl_typedefs.h
  src/libANGLE/renderer/gl/wgl/wgl_utils.cpp
  src/libANGLE/renderer/gl/wgl/wgl_utils.h
  src/third_party/khronos/GL/wglext.h
)

set(libangle_gl_glx_sources
  src/libANGLE/renderer/gl/glx/DisplayGLX.cpp
  src/libANGLE/renderer/gl/glx/DisplayGLX.h
  src/libANGLE/renderer/gl/glx/FunctionsGLX.cpp
  src/libANGLE/renderer/gl/glx/FunctionsGLX.h
  src/libANGLE/renderer/gl/glx/RendererGLX.h
  src/libANGLE/renderer/gl/glx/RendererGLX.cpp
  src/libANGLE/renderer/gl/glx/PbufferSurfaceGLX.cpp
  src/libANGLE/renderer/gl/glx/PbufferSurfaceGLX.h
  src/libANGLE/renderer/gl/glx/SurfaceGLX.h
  src/libANGLE/renderer/gl/glx/WindowSurfaceGLX.cpp
  src/libANGLE/renderer/gl/glx/WindowSurfaceGLX.h
  src/libANGLE/renderer/gl/glx/functionsglx_typedefs.h
  src/libANGLE/renderer/gl/glx/platform_glx.h
)

set(libangle_gl_egl_sources
  src/libANGLE/renderer/gl/egl/ContextEGL.cpp
  src/libANGLE/renderer/gl/egl/ContextEGL.h
  src/libANGLE/renderer/gl/egl/DisplayEGL.cpp
  src/libANGLE/renderer/gl/egl/DisplayEGL.h
  src/libANGLE/renderer/gl/egl/ExternalImageSiblingEGL.h
  src/libANGLE/renderer/gl/egl/egl_utils.cpp
  src/libANGLE/renderer/gl/egl/egl_utils.h
  src/libANGLE/renderer/gl/egl/FunctionsEGL.cpp
  src/libANGLE/renderer/gl/egl/FunctionsEGL.h
  src/libANGLE/renderer/gl/egl/ImageEGL.cpp
  src/libANGLE/renderer/gl/egl/ImageEGL.h
  src/libANGLE/renderer/gl/egl/functionsegl_typedefs.h
  src/libANGLE/renderer/gl/egl/PbufferSurfaceEGL.cpp
  src/libANGLE/renderer/gl/egl/PbufferSurfaceEGL.h
  src/libANGLE/renderer/gl/egl/RendererEGL.cpp
  src/libANGLE/renderer/gl/egl/RendererEGL.h
  src/libANGLE/renderer/gl/egl/SurfaceEGL.cpp
  src/libANGLE/renderer/gl/egl/SurfaceEGL.h
  src/libANGLE/renderer/gl/egl/SyncEGL.cpp
  src/libANGLE/renderer/gl/egl/SyncEGL.h
  src/libANGLE/renderer/gl/egl/WindowSurfaceEGL.cpp
  src/libANGLE/renderer/gl/egl/WindowSurfaceEGL.h
)
set(libangle_gl_egl_dl_sources
  src/libANGLE/renderer/gl/egl/FunctionsEGLDL.cpp
  src/libANGLE/renderer/gl/egl/FunctionsEGLDL.h
)

set(libangle_gl_ozone_sources
  src/libANGLE/renderer/gl/egl/ozone/DisplayOzone.cpp
  src/libANGLE/renderer/gl/egl/ozone/DisplayOzone.h
  src/libANGLE/renderer/gl/egl/ozone/SurfaceOzone.cpp
  src/libANGLE/renderer/gl/egl/ozone/SurfaceOzone.h
)

set(libangle_gl_egl_android_sources
  src/libANGLE/renderer/gl/egl/android/DisplayAndroid.cpp
  src/libANGLE/renderer/gl/egl/android/DisplayAndroid.h
  src/libANGLE/renderer/gl/egl/android/NativeBufferImageSiblingAndroid.cpp
  src/libANGLE/renderer/gl/egl/android/NativeBufferImageSiblingAndroid.h
)

set(libangle_gl_cgl_sources
  src/libANGLE/renderer/gl/cgl/DisplayCGL.mm
  src/libANGLE/renderer/gl/cgl/DisplayCGL.h
  src/libANGLE/renderer/gl/cgl/IOSurfaceSurfaceCGL.mm
  src/libANGLE/renderer/gl/cgl/IOSurfaceSurfaceCGL.h
  src/libANGLE/renderer/gl/cgl/RendererCGL.mm
  src/libANGLE/renderer/gl/cgl/RendererCGL.h
  src/libANGLE/renderer/gl/cgl/PbufferSurfaceCGL.mm
  src/libANGLE/renderer/gl/cgl/PbufferSurfaceCGL.h
  src/libANGLE/renderer/gl/cgl/WindowSurfaceCGL.mm
  src/libANGLE/renderer/gl/cgl/WindowSurfaceCGL.h
)

set(libangle_vulkan_sources
  src/libANGLE/renderer/vulkan/BufferVk.cpp
  src/libANGLE/renderer/vulkan/BufferVk.h
  src/libANGLE/renderer/vulkan/CommandGraph.cpp
  src/libANGLE/renderer/vulkan/CommandGraph.h
  src/libANGLE/renderer/vulkan/CompilerVk.cpp
  src/libANGLE/renderer/vulkan/CompilerVk.h
  src/libANGLE/renderer/vulkan/ContextVk.cpp
  src/libANGLE/renderer/vulkan/ContextVk.h
  src/libANGLE/renderer/vulkan/DeviceVk.cpp
  src/libANGLE/renderer/vulkan/DeviceVk.h
  src/libANGLE/renderer/vulkan/DisplayVk.cpp
  src/libANGLE/renderer/vulkan/DisplayVk.h
  src/libANGLE/renderer/vulkan/FenceNVVk.cpp
  src/libANGLE/renderer/vulkan/FenceNVVk.h
  src/libANGLE/renderer/vulkan/FramebufferVk.cpp
  src/libANGLE/renderer/vulkan/FramebufferVk.h
  src/libANGLE/renderer/vulkan/GlslangWrapper.cpp
  src/libANGLE/renderer/vulkan/GlslangWrapper.h
  src/libANGLE/renderer/vulkan/ImageVk.cpp
  src/libANGLE/renderer/vulkan/ImageVk.h
  src/libANGLE/renderer/vulkan/ProgramVk.cpp
  src/libANGLE/renderer/vulkan/ProgramVk.h
  src/libANGLE/renderer/vulkan/ProgramPipelineVk.cpp
  src/libANGLE/renderer/vulkan/ProgramPipelineVk.h
  src/libANGLE/renderer/vulkan/QueryVk.cpp
  src/libANGLE/renderer/vulkan/QueryVk.h
  src/libANGLE/renderer/vulkan/RenderbufferVk.cpp
  src/libANGLE/renderer/vulkan/RenderbufferVk.h
  src/libANGLE/renderer/vulkan/RendererVk.cpp
  src/libANGLE/renderer/vulkan/RendererVk.h
  src/libANGLE/renderer/vulkan/RenderTargetVk.cpp
  src/libANGLE/renderer/vulkan/RenderTargetVk.h
  src/libANGLE/renderer/vulkan/SamplerVk.cpp
  src/libANGLE/renderer/vulkan/SamplerVk.h
  src/libANGLE/renderer/vulkan/SecondaryCommandBuffer.cpp
  src/libANGLE/renderer/vulkan/SecondaryCommandBuffer.h
  src/libANGLE/renderer/vulkan/ShaderVk.cpp
  src/libANGLE/renderer/vulkan/ShaderVk.h
  src/libANGLE/renderer/vulkan/SurfaceVk.cpp
  src/libANGLE/renderer/vulkan/SurfaceVk.h
  src/libANGLE/renderer/vulkan/SyncVk.cpp
  src/libANGLE/renderer/vulkan/SyncVk.h
  src/libANGLE/renderer/vulkan/TextureVk.cpp
  src/libANGLE/renderer/vulkan/TextureVk.h
  src/libANGLE/renderer/vulkan/TransformFeedbackVk.cpp
  src/libANGLE/renderer/vulkan/TransformFeedbackVk.h
  src/libANGLE/renderer/vulkan/UtilsVk.cpp
  src/libANGLE/renderer/vulkan/UtilsVk.h
  src/libANGLE/renderer/vulkan/VertexArrayVk.cpp
  src/libANGLE/renderer/vulkan/VertexArrayVk.h
  src/libANGLE/renderer/vulkan/vk_cache_utils.cpp
  src/libANGLE/renderer/vulkan/vk_cache_utils.h
  src/libANGLE/renderer/vulkan/vk_caps_utils.cpp
  src/libANGLE/renderer/vulkan/vk_caps_utils.h
  src/libANGLE/renderer/vulkan/vk_format_table_autogen.cpp
  src/libANGLE/renderer/vulkan/vk_format_utils.h
  src/libANGLE/renderer/vulkan/vk_format_utils.cpp
  src/libANGLE/renderer/vulkan/vk_helpers.cpp
  src/libANGLE/renderer/vulkan/vk_helpers.h
  src/libANGLE/renderer/vulkan/vk_internal_shaders_autogen.h
  src/libANGLE/renderer/vulkan/vk_internal_shaders_autogen.cpp
  src/libANGLE/renderer/vulkan/vk_mandatory_format_support_table_autogen.cpp
  src/libANGLE/renderer/vulkan/vk_utils.cpp
  src/libANGLE/renderer/vulkan/vk_utils.h
  src/libANGLE/renderer/vulkan/vk_wrapper.h
)

set(libangle_vulkan_android_sources
  src/libANGLE/renderer/vulkan/android/DisplayVkAndroid.cpp
  src/libANGLE/renderer/vulkan/android/DisplayVkAndroid.h
  src/libANGLE/renderer/vulkan/android/HardwareBufferImageSiblingVkAndroid.cpp
  src/libANGLE/renderer/vulkan/android/HardwareBufferImageSiblingVkAndroid.h
  src/libANGLE/renderer/vulkan/android/WindowSurfaceVkAndroid.cpp
  src/libANGLE/renderer/vulkan/android/WindowSurfaceVkAndroid.h
)

set(libangle_vulkan_win32_sources
  src/libANGLE/renderer/vulkan/win32/DisplayVkWin32.cpp
  src/libANGLE/renderer/vulkan/win32/DisplayVkWin32.h
  src/libANGLE/renderer/vulkan/win32/WindowSurfaceVkWin32.cpp
  src/libANGLE/renderer/vulkan/win32/WindowSurfaceVkWin32.h
)

set(libangle_vulkan_xcb_sources
  src/libANGLE/renderer/vulkan/xcb/DisplayVkXcb.cpp
  src/libANGLE/renderer/vulkan/xcb/DisplayVkXcb.h
  src/libANGLE/renderer/vulkan/xcb/WindowSurfaceVkXcb.cpp
  src/libANGLE/renderer/vulkan/xcb/WindowSurfaceVkXcb.h
)

set(libangle_vulkan_fuchsia_sources
  src/libANGLE/renderer/vulkan/fuchsia/DisplayVkFuchsia.cpp
  src/libANGLE/renderer/vulkan/fuchsia/DisplayVkFuchsia.h
  src/libANGLE/renderer/vulkan/fuchsia/WindowSurfaceVkFuchsia.cpp
  src/libANGLE/renderer/vulkan/fuchsia/WindowSurfaceVkFuchsia.h
)

set(libangle_null_sources
  src/libANGLE/renderer/null/BufferNULL.cpp
  src/libANGLE/renderer/null/BufferNULL.h
  src/libANGLE/renderer/null/CompilerNULL.cpp
  src/libANGLE/renderer/null/CompilerNULL.h
  src/libANGLE/renderer/null/ContextNULL.cpp
  src/libANGLE/renderer/null/ContextNULL.h
  src/libANGLE/renderer/null/DeviceNULL.cpp
  src/libANGLE/renderer/null/DeviceNULL.h
  src/libANGLE/renderer/null/DisplayNULL.cpp
  src/libANGLE/renderer/null/DisplayNULL.h
  src/libANGLE/renderer/null/FenceNVNULL.cpp
  src/libANGLE/renderer/null/FenceNVNULL.h
  src/libANGLE/renderer/null/FramebufferNULL.cpp
  src/libANGLE/renderer/null/FramebufferNULL.h
  src/libANGLE/renderer/null/ImageNULL.cpp
  src/libANGLE/renderer/null/ImageNULL.h
  src/libANGLE/renderer/null/PathNULL.cpp
  src/libANGLE/renderer/null/PathNULL.h
  src/libANGLE/renderer/null/ProgramNULL.cpp
  src/libANGLE/renderer/null/ProgramNULL.h
  src/libANGLE/renderer/null/ProgramPipelineNULL.cpp
  src/libANGLE/renderer/null/ProgramPipelineNULL.h
  src/libANGLE/renderer/null/QueryNULL.cpp
  src/libANGLE/renderer/null/QueryNULL.h
  src/libANGLE/renderer/null/RenderbufferNULL.cpp
  src/libANGLE/renderer/null/RenderbufferNULL.h
  src/libANGLE/renderer/null/SamplerNULL.cpp
  src/libANGLE/renderer/null/SamplerNULL.h
  src/libANGLE/renderer/null/ShaderNULL.cpp
  src/libANGLE/renderer/null/ShaderNULL.h
  src/libANGLE/renderer/null/SurfaceNULL.cpp
  src/libANGLE/renderer/null/SurfaceNULL.h
  src/libANGLE/renderer/null/SyncNULL.cpp
  src/libANGLE/renderer/null/SyncNULL.h
  src/libANGLE/renderer/null/TextureNULL.cpp
  src/libANGLE/renderer/null/TextureNULL.h
  src/libANGLE/renderer/null/TransformFeedbackNULL.cpp
  src/libANGLE/renderer/null/TransformFeedbackNULL.h
  src/libANGLE/renderer/null/VertexArrayNULL.cpp
  src/libANGLE/renderer/null/VertexArrayNULL.h
)

set(libglesv2_sources
  src/common/angleutils.h
  src/common/debug.h
  src/libGLESv2/entry_points_egl.cpp
  src/libGLESv2/entry_points_egl.h
  src/libGLESv2/entry_points_egl_ext.cpp
  src/libGLESv2/entry_points_egl_ext.h
  src/libGLESv2/entry_points_enum_autogen.h
  src/libGLESv2/entry_points_gles_1_0_autogen.cpp
  src/libGLESv2/entry_points_gles_1_0_autogen.h
  src/libGLESv2/entry_points_gles_2_0_autogen.cpp
  src/libGLESv2/entry_points_gles_2_0_autogen.h
  src/libGLESv2/entry_points_gles_3_0_autogen.cpp
  src/libGLESv2/entry_points_gles_3_0_autogen.h
  src/libGLESv2/entry_points_gles_3_1_autogen.cpp
  src/libGLESv2/entry_points_gles_3_1_autogen.h
  src/libGLESv2/entry_points_gles_ext_autogen.cpp
  src/libGLESv2/entry_points_gles_ext_autogen.h
  src/libGLESv2/entry_points_utils.h
  src/libGLESv2/global_state.cpp
  src/libGLESv2/global_state.h
  src/libGLESv2/libGLESv2_autogen.cpp
  src/libGLESv2/libGLESv2.rc
  src/libGLESv2/proc_table.h
  src/libGLESv2/proc_table_autogen.cpp
  src/libGLESv2/resource.h
)

set(libglesv1_cm_sources
  src/libGLESv1_CM/libGLESv1_CM.cpp
  src/libGLESv1_CM/libGLESv1_CM.def
  src/libGLESv1_CM/libGLESv1_CM.rc
  src/libGLESv1_CM/resource.h
)

set(libegl_sources
  src/libEGL/libEGL.cpp
  src/libEGL/libEGL.rc
  src/libEGL/resource.h
)

#
# Util
#

set(util_sources
  util/com_utils.h
  util/keyboard.h
  util/geometry_utils.cpp
  util/geometry_utils.h
  util/mouse.h
  util/random_utils.cpp
  util/random_utils.h
  util/shader_utils.cpp
  util/shader_utils.h
  util/system_utils.h
  util/util_export.h
  util/util_gl.h
  util/Event.h
  util/EGLWindow.cpp
  util/EGLWindow.h
  util/Matrix.cpp
  util/Matrix.h
  util/OSPixmap.h
  util/OSWindow.cpp
  util/OSWindow.h
  util/Timer.h
)

set(util_win_sources
  util/windows/win32/Win32_system_utils.cpp
  util/windows/win32/Win32Pixmap.cpp
  util/windows/win32/Win32Pixmap.h
  util/windows/win32/Win32Window.cpp
  util/windows/win32/Win32Window.h
  util/windows/Windows_system_utils.cpp
  util/windows/WindowsTimer.cpp
  util/windows/WindowsTimer.h
)

set(util_win_shared_sources
  util/windows/WGLWindow.cpp
  util/windows/WGLWindow.h
)

set(util_winrt_sources
  util/windows/winrt/WinRT_system_utils.cpp
  util/windows/winrt/WinRTPixmap.cpp
  util/windows/winrt/WinRTWindow.cpp
  util/windows/winrt/WinRTWindow.h
  util/windows/Windows_system_utils.cpp
  util/windows/WindowsTimer.cpp
  util/windows/WindowsTimer.h
)

set(util_linux_sources
  util/posix/PosixTimer.cpp
  util/posix/PosixTimer.h
  util/posix/Posix_system_utils.cpp
)

set(util_x11_sources
  util/x11/X11Pixmap.cpp
  util/x11/X11Pixmap.h
  util/x11/X11Window.cpp
  util/x11/X11Window.h
)

set(util_fuchsia_sources
  util/posix/PosixTimer.cpp
  util/posix/PosixTimer.h
  util/posix/Posix_system_utils.cpp
  util/fuchsia/ScenicWindow.cpp
  util/fuchsia/ScenicWindow.h
)

set(util_ozone_sources
  util/ozone/OzonePixmap.cpp
  util/ozone/OzoneWindow.cpp
  util/ozone/OzoneWindow.h
)

set(util_osx_sources
  util/osx/OSXTimer.cpp
  util/osx/OSXTimer.h
  util/osx/OSXPixmap.mm
  util/osx/OSXPixmap.h
  util/osx/OSXWindow.mm
  util/osx/OSXWindow.h
  util/posix/Posix_system_utils.cpp
)

set(util_android_sources
  util/android/AndroidPixmap.cpp
  util/android/AndroidWindow.cpp
  util/android/AndroidWindow.h
  util/android/third_party/android_native_app_glue.c
  util/android/third_party/android_native_app_glue.h
)


########################################################################
#
# ANGLE Library Configuration
#
# Debug
# - ANGLE_DISABLE_POOL_ALLOC
# - ANGLE_ENABLE_DEBUG_ANNOTATIONS
# - ANGLE_ENABLE_RELEASE_ASSERTS
#
# Configuration
# - ANGLE_ENABLE_D3D9
# - ANGLE_ENABLE_D3D11
# - ANGLE_ENABLE_OPENGL
# - ANGLE_USE_X11
# - ANGLE_ENABLE_OPENGL_NULL
# - ANGLE_ENABLE_VULKAN
# - ANGLE_USE_CUSTOM_VULKAN_CMD_BUFFERS
# - ANGLE_ENABLE_NULL
#
########################################################################

#
# Build defaults
#

if(WIN32)
  set(ANGLE_ENABLE_D3D9 TRUE)
endif()
if(UNIX)
  set(ANGLE_ENABLE_GL TRUE)
endif()

#
# Base includes and compiler flags
#

set(CMAKE_POSITION_INDEPENDENT_CODE ON)
include_directories(src include src/common/third_party/base)
add_definitions(-DANGLE_EGL_LIBRARY_NAME=\"libEGL\")
add_definitions(-DANGLE_GLESV2_LIBRARY_NAME=\"libGLESv2\")
add_compile_options(-std=c++14 -fno-exceptions -fno-rtti)
add_compile_options(-fvisibility-inlines-hidden)

set(no_gl_prototypes
  -DGL_GLES_PROTOTYPES=0 -DEGL_EGL_PROTOTYPES=0)
set(gl_prototypes
  -DGL_GLEXT_PROTOTYPES -DEGL_EGLEXT_PROTOTYPES
  -DGL_GLES_PROTOTYPES=1 -DEGL_EGL_PROTOTYPES=1)
set(egl_api_visibility_unspec -DEGLAPI=)
set(gl_api_visibility_unspec -DGL_APICALL= -DGL_API=)
set(egl_api_visibility_default
  -DEGLAPI=__attribute__\(\(visibility\(\"default\"\)\)\))
set(gl_api_default
  -DGL_APICALL=__attribute__\(\(visibility\(\"default\"\)\)\)
  -DGL_API=__attribute__\(\(visibility\(\"default\"\)\)\))

# ANGLE build steps control symbol visibility using visibility attributes
# and compiler flags, however, adding -fvisibility=hidden currently results
# in undefined symbols during link. Uncomment this line to see:
#add_compile_options(-fvisibility=hidden)
set(target_link_options -Wl,--no-undefined)

# The EXPORT macros are required by EGL_static, angle_util_static,
# libGLESv2_static and libGLESv1_CM_static
#add_definitions(-DANGLE_EXPORT= -DANGLE_UTIL_EXPORT=)

#
# Compiler specific flags
#

if("${CMAKE_SIZEOF_VOID_P}" STREQUAL "4")
  add_definitions(-DANGLE_IS_32_BIT_CPU)
endif()
if("${CMAKE_SIZEOF_VOID_P}" STREQUAL "8")
  add_definitions(-DANGLE_IS_64_BIT_CPU)
endif()
if("${CMAKE_CXX_COMPILER_ID}" STREQUAL "GNU")
  add_definitions(-DCOMPILER_GCC)
endif()

#
# Configuration options
#

if(ANGLE_FORCE_THREAD_SAFETY)
  add_definitions(-DANGLE_FORCE_THREAD_SAFETY=1)
endif()
if(ANGLE_ENABLE_VULKAN)
  if(ANGLE_ENABLE_VULKAN_GPU_TRACE_EVENTS)
    add_definitions(-DANGLE_ENABLE_VULKAN_GPU_TRACE_EVENTS=1)
  endif()
  if(ANGLE_VULKAN_CONFORMANT_CONFIGS_ONLY)
    add_definitions(-DANGLE_VULKAN_CONFORMANT_CONFIGS_ONLY=1)
  endif()
endif()
if (ANGLE_ENABLE_TRACE)
  add_definitions(-DANGLE_ENABLE_DEBUG_TRACE=1)
endif()

#
# D3D9 backend
#

if(ANGLE_ENABLE_D3D9)
  if(WIN32)
    find_library(D3D9_LIB d3d9)
    find_library(D3D9_COMPILER d3dcompiler_47)
    list(APPEND ANGLE_OS_LIBS ${D3D9_LIB} ${D3D9_COMPILER})
    add_definitions(-DANGLE_ENABLE_D3D9)
  endif()
endif()

#
# D3D11 backend
#

if(ANGLE_ENABLE_D3D11)
  if(WIN32)
    find_library(DXGUID_LIB dxguid)
    list(APPEND ANGLE_OS_LIBS ${DXGUID_LIB})
    add_definitions(-DANGLE_ENABLE_D3D11)
  endif()
endif()

#
# OpenGL backend
#

if(ANGLE_ENABLE_GL)
  if(APPLE)
    find_library(COCOA_LIB Cocoa)
    find_library(IOSURFACE_LIB IOSurface)
    find_library(QUARTZCORE_LIB QuartzCore)
    find_library(CORE_FOUNDATION_LIB CoreFoundation)
    find_library(CORE_GRAPHICS_LIB CoreGraphics)
    find_library(IOKIT_LIB IOKit)
    list(APPEND ANGLE_OS_LIBS ${COCOA_LIB} ${IOSURFACE_LIB} ${QUARTZCORE_LIB})
    list(APPEND ANGLE_OS_LIBS ${CORE_FOUNDATION_LIB} ${CORE_GRAPHICS_LIB})
    list(APPEND ANGLE_OS_LIBS ${IOKIT_LIB} ${OPENGL_LIB})
    if(ANGLE_LINK_GLX)
      find_library(OPENGL_LIB OpenGL)
      list(APPEND ANGLE_OS_LIBS ${OPENGL_LIB})
    endif()
    add_definitions(-DANGLE_ENABLE_OPENGL)
  elseif(UNIX)
    find_library(X11_LIB X11)
    find_library(XINPUT_LIB Xi)
    find_library(XEXT_LIB Xext)
    find_library(JSONCPP_LIB jsoncpp)
    find_library(PCI_LIB pci)
    find_package(Threads REQUIRED)
    include_directories(/usr/include/jsoncpp)
    list(APPEND ANGLE_OS_LIBS ${X11_LIB} ${XINPUT_LIB} ${XEXT_LIB})
    list(APPEND ANGLE_OS_LIBS ${JSONCPP_LIBRARY} ${PCI_LIB})
    list(APPEND ANGLE_OS_LIBS Threads::Threads dl)
    if(ANGLE_LINK_GLX)
      find_library(OPENGL_LIB GL)
      list(APPEND ANGLE_OS_LIBS ${OPENGL_LIB})
    endif()
    add_definitions(-DANGLE_ENABLE_OPENGL -DANGLE_USE_X11)
  elseif(WIN32)
    find_library(OPENGL_LIB OpenGL32)
    add_definitions(-DANGLE_ENABLE_OPENGL)
    list(APPEND ANGLE_OS_LIBS ${OPENGL_LIB})
  endif()
  if(ANGLE_ENABLE_OPENGL_NULL)
    add_definitions(-DANGLE_ENABLE_OPENGL_NULL)
  endif()
endif()

#
# Null backend
#

if(ANGLE_ENABLE_NULL)
add_definitions(-DANGLE_ENABLE_NULL)
endif()


########################################################################
#
# ANGLE Library build
#
########################################################################

#
# angle_system_utils (source set)
#

add_library(angle_system_utils OBJECT ${angle_system_utils_sources})

#
# xxhash (source set)
#

add_library(xxhash OBJECT ${xxhash_sources})

#
# angle_common (static library)
#

add_library(angle_common STATIC ${libangle_common_sources})

#
# translator (static library)
#

add_library(translator STATIC ${angle_translator_sources}
  ${angle_translator_essl_sources} ${angle_translator_glsl_sources})
add_definitions(-DANGLE_ENABLE_ESSL -DANGLE_ENABLE_GLSL)

#
# preprocessor (static library)
#

add_library(preprocessor STATIC ${angle_preprocessor_sources})

#
# angle_image_util (static library)
#

add_library(angle_image_util STATIC ${libangle_image_util_sources})

#
# angle_gpu_info_util (static library)
#

if(WIN32)
  list(APPEND libangle_gpu_info_util_sources ${libangle_gpu_info_util_win_sources})
  add_definitions(-DGPU_INFO_USE_SETUPAPI)
elseif(APPLE)
  list(APPEND libangle_gpu_info_util_sources ${libangle_gpu_info_util_mac_sources})
elseif(UNIX)
  list(APPEND libangle_gpu_info_util_sources ${libangle_gpu_info_util_linux_sources})
  list(APPEND libangle_gpu_info_util_sources ${libangle_gpu_info_util_libpci_sources})
  add_definitions(-DGPU_INFO_USE_LIBPCI)
  list(APPEND libangle_gpu_info_util_sources ${libangle_gpu_info_util_x11_sources})
  add_definitions(-DGPU_INFO_USE_X11)
endif()
add_library(angle_gpu_info_util STATIC ${libangle_gpu_info_util_sources})

#
# angle_util_loader (source set)
#

add_library(angle_util_loader OBJECT
  util/egl_loader_autogen.cpp
  util/gles_loader_autogen.cpp)
target_include_directories(angle_util_loader PRIVATE .)
target_compile_definitions(angle_util_loader PRIVATE -DANGLE_USE_UTIL_LOADER)
target_compile_definitions(angle_util_loader PRIVATE ${no_gl_prototypes})

#
# angle_util (shared library)
#

if(APPLE)
  list(APPEND util_sources ${util_osx_sources})
elseif(UNIX)
  list(APPEND util_sources ${util_linux_sources} ${util_x11_sources})
elseif(WIN32)
  list(APPEND util_sources ${util_win_sources} ${util_win_shared_sources})
endif()
add_library(angle_util SHARED ${util_sources}
  $<TARGET_OBJECTS:angle_util_loader>
  $<TARGET_OBJECTS:angle_system_utils>
  $<TARGET_OBJECTS:xxhash>
)
target_include_directories(angle_util PRIVATE .)
target_compile_definitions(angle_util PRIVATE -DLIBANGLE_UTIL_IMPLEMENTATION)
target_compile_definitions(angle_util PRIVATE -DANGLE_USE_UTIL_LOADER)
target_compile_definitions(angle_util PRIVATE ${no_gl_prototypes})
target_link_libraries(angle_util PRIVATE angle_common ${ANGLE_OS_LIBS})

#
# feature_support (shared library)
#

add_library(feature_support SHARED
  src/feature_support_util/feature_support_util.cpp
  src/feature_support_util/feature_support_util.h
  $<TARGET_OBJECTS:angle_system_utils>
  $<TARGET_OBJECTS:xxhash>
)
target_compile_definitions(feature_support PRIVATE -DANGLE_FEATURE_UTIL_LOG_VERBOSE)
target_compile_definitions(feature_support PRIVATE -DLIBFEATURE_SUPPORT_IMPLEMENTATION)
target_link_libraries(feature_support PRIVATE ${target_link_options})
target_link_libraries(feature_support PRIVATE angle_gpu_info_util angle_common jsoncpp)
target_link_libraries(feature_support PRIVATE ${ANGLE_OS_LIBS})

#
# ANGLE (static library)
#

if(ANGLE_ENABLE_D3D9)
  list(APPEND libangle_sources ${libangle_d3d_shared_sources})
  list(APPEND libangle_sources ${libangle_d3d9_sources})
endif()
if(ANGLE_ENABLE_D3D11)
  list(APPEND libangle_sources ${libangle_d3d11_sources})
  list(APPEND libangle_sources ${libangle_d3d11_win32_sources})
endif()
if(ANGLE_ENABLE_VULKAN)
  list(APPEND libangle_sources ${libangle_vulkan_sources})
  if(WIN32)
    list(APPEND libangle_sources ${libangle_vulkan_win32_sources})
  elseif(UNIX)
    list(APPEND libangle_sources ${libangle_vulkan_xcb_sources})
  endif()
endif()
if(ANGLE_ENABLE_GL)
  list(APPEND libangle_sources ${libangle_gl_sources})
  if(APPLE)
    list(APPEND libangle_sources ${libangle_gl_cgl_sources})
  elseif(UNIX)
    list(APPEND libangle_sources ${libangle_gl_glx_sources})
  elseif(WIN32)
    list(APPEND libangle_sources ${libangle_gl_wgl_sources})
  endif()
  if(ANGLE_ENABLE_OPENGL_NULL)
    list(APPEND libangle_sources ${libangle_gl_null_sources})
  endif()
endif()
if(ANGLE_ENABLE_NULL)
  list(APPEND libangle_sources ${libangle_null_sources})
endif()
add_library(ANGLE STATIC ${libangle_sources})
add_dependencies(ANGLE commit_id_file)
target_compile_definitions(ANGLE PRIVATE -DLIBANGLE_IMPLEMENTATION)
target_link_libraries(ANGLE PRIVATE ${target_link_options})
target_link_libraries(ANGLE PRIVATE ${ANGLE_OS_LIBS})

#
# commit_id (generated file)
#

set(${PROJECT_SOURCE_DIR}/src/commit.h)
set(commit_id_out_dir ${PROJECT_BINARY_DIR}/angle/id)
set(commit_id_out_file ${commit_id_out_dir}/commit.h)
set(commit_id_cmd_args gen ${PROJECT_SOURCE_DIR} ${commit_id_out_file})
add_custom_target(commit_id_dir COMMAND ${CMAKE_COMMAND} -E make_directory ${commit_id_out_dir} DEPENDS .git/HEAD)
add_custom_target(commit_id_file COMMAND python ${PROJECT_SOURCE_DIR}/src/commit_id.py ${commit_id_cmd_args} DEPENDS .git/HEAD)
add_dependencies(commit_id_file commit_id_dir)
include_directories(${PROJECT_BINARY_DIR}/angle)

#
# GLESv2 (shared library)
#

if(WIN32)
list(libglesv2_sources APPEND src/libGLESv2/libGLESv2_autogen.def)
endif()
add_library(GLESv2 SHARED ${libglesv2_sources}
  $<TARGET_OBJECTS:angle_system_utils>
  $<TARGET_OBJECTS:xxhash>
)
target_compile_definitions(GLESv2 PRIVATE -DLIBGLESV2_IMPLEMENTATION)
target_compile_definitions(GLESv2 PRIVATE ${gl_prototypes})
target_compile_definitions(GLESv2 PRIVATE ${gl_api_visibility_default})
target_compile_definitions(GLESv2 PRIVATE ${egl_api_visibility_unspec})
target_link_libraries(GLESv2 PRIVATE ANGLE angle_gpu_info_util
  angle_image_util translator preprocessor angle_common ${ANGLE_OS_LIBS})
target_link_libraries(GLESv2 PRIVATE ${target_link_options})

#
# GLESv1_CM (shared library)
#

add_library(GLESv1_CM SHARED ${libglesv1_cm_sources})
target_compile_definitions(GLESv1_CM PRIVATE ${gl_prototypes})
target_compile_definitions(GLESv1_CM PRIVATE ${gl_api_visibility_default})
target_compile_definitions(GLESv1_CM PRIVATE ${egl_api_visibility_unspec})
target_link_libraries(GLESv1_CM PRIVATE ${target_link_options})
target_link_libraries(GLESv1_CM PRIVATE GLESv2 ${ANGLE_OS_LIBS})

#
# EGL_egl_loader (source set)
#

add_library(EGL_egl_loader OBJECT
  src/libEGL/egl_loader_autogen.cpp
  src/libEGL/egl_loader_autogen.h)
target_compile_definitions(EGL_egl_loader PRIVATE -DANGLE_USE_EGL_LOADER)
target_compile_definitions(EGL_egl_loader PRIVATE ${gl_prototypes})
target_compile_definitions(EGL_egl_loader PRIVATE ${egl_api_visibility_default})

#
# EGL (shared library)
#

if(WIN32)
list(EGL APPEND src/libEGL/libEGL.def)
endif()
add_library(EGL SHARED ${libegl_sources}
  $<TARGET_OBJECTS:EGL_egl_loader>
  $<TARGET_OBJECTS:angle_system_utils>
)
target_compile_definitions(EGL PRIVATE -DLIBEGL_IMPLEMENTATION)
target_compile_definitions(EGL PRIVATE -DANGLE_USE_EGL_LOADER)
target_compile_definitions(EGL PRIVATE ${gl_prototypes})
target_compile_definitions(EGL PRIVATE ${gl_api_visibility_unspec})
target_compile_definitions(EGL PRIVATE ${egl_api_visibility_default})
target_link_libraries(EGL PRIVATE ${target_link_options})
target_link_libraries(EGL PRIVATE ${ANGLE_OS_LIBS})


########################################################################
#
# ANGLE Samples
#
########################################################################

#
# shader_translator (executable)
#

add_executable(shader_translator samples/shader_translator/shader_translator.cpp)
target_link_libraries(shader_translator ANGLE angle_gpu_info_util
  angle_image_util translator preprocessor angle_common)

#
# sample_util (static library)
#

add_library(sample_util STATIC
  samples/sample_util/SampleApplication.cpp
  samples/sample_util/SampleApplication.h
  samples/sample_util/texture_utils.cpp
  samples/sample_util/texture_utils.h
  samples/sample_util/tga_utils.cpp
  samples/sample_util/tga_utils.h)
target_include_directories(sample_util PRIVATE .)
target_compile_definitions(sample_util PRIVATE -DANGLE_USE_UTIL_LOADER)
target_compile_definitions(sample_util PRIVATE ${no_gl_prototypes})

#
# samples (executable)
#

function(sample NAME SOURCE)
  add_executable(${NAME} ${SOURCE}
    $<TARGET_OBJECTS:angle_system_utils>
  )
  target_include_directories(${NAME} PRIVATE . samples/sample_util)
  target_compile_definitions(${NAME} PRIVATE -DANGLE_USE_UTIL_LOADER)
  target_compile_definitions(${NAME} PRIVATE ${no_gl_prototypes})
  target_link_libraries(${NAME} PRIVATE ${target_link_options})
  target_link_libraries(${NAME} PRIVATE sample_util angle_util)
  target_link_libraries(${NAME} PRIVATE ${ANGLE_OS_LIBS})
endfunction(sample)

sample(hello_triangle samples/hello_triangle/HelloTriangle.cpp)
sample(mip_map_2d samples/mip_map_2d/MipMap2D.cpp)
sample(multiple_draw_buffers samples/multiple_draw_buffers/MultipleDrawBuffers.cpp)
sample(multi_texture samples/multi_texture/MultiTexture.cpp)
sample(multiview samples/multiview/Multiview.cpp)
sample(multi_window samples/multi_window/MultiWindow.cpp)
sample(particle_system samples/particle_system/ParticleSystem.cpp)
sample(post_sub_buffer samples/post_sub_buffer/PostSubBuffer.cpp)
sample(simple_instancing samples/simple_instancing/SimpleInstancing.cpp)
sample(simple_texture_2d samples/simple_texture_2d/SimpleTexture2D.cpp)
sample(simple_texture_cubemap samples/simple_texture_cubemap/SimpleTextureCubemap.cpp)
sample(stencil_operations samples/stencil_operations/StencilOperations.cpp)
sample(tex_redef_microbench samples/tex_redef_microbench/TexRedefMicroBench.cpp)
sample(texture_wrap samples/texture_wrap/TextureWrap.cpp)
sample(tri_fan_microbench samples/tri_fan_microbench/TriFanMicroBench.cpp)
sample(WindowTest samples/WindowTest/WindowTest.cpp)
