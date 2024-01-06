<!--
# Copyright (c) 2023, NVIDIA CORPORATION & AFFILIATES. All rights reserved.
#
# Redistribution and use in source and binary forms, with or without
# modification, are permitted provided that the following conditions
# are met:
#  * Redistributions of source code must retain the above copyright
#    notice, this list of conditions and the following disclaimer.
#  * Redistributions in binary form must reproduce the above copyright
#    notice, this list of conditions and the following disclaimer in the
#    documentation and/or other materials provided with the distribution.
#  * Neither the name of NVIDIA CORPORATION nor the names of its
#    contributors may be used to endorse or promote products derived
#    from this software without specific prior written permission.
#
# THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS ``AS IS'' AND ANY
# EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE
# IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR
# PURPOSE ARE DISCLAIMED.  IN NO EVENT SHALL THE COPYRIGHT OWNER OR
# CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL,
# EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO,
# PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR
# PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY
# OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT
# (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE
# OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
-->

[![License](https://img.shields.io/badge/License-BSD3-lightgrey.svg)](https://opensource.org/licenses/BSD-3-Clause)

# Example C# Client Using Generated GRPC API

## Prerequisites

Required NuGet Packages:\
`Grpc.Tools`, used to generate C# code for gRPC services.\
`Grpc.Net.Client`, used to communicate with the server.\
`Google.Protobuf`, used to read and write the protocol buffer messages.


## Generating C# GRPC client stub

Clone the [triton-inference-server/common](https://github.com/triton-inference-server/common/)
repository:

```
git clone https://github.com/triton-inference-server/common/ -b <common-repo-branch> common-repo
```

\<common-repo-branch\> should be the version of the Triton server that you
intend to use (e.g. r23.12).

Copy __*.proto__ files to ./Protos

```
$ cd your-project-folder
$ mkdir Protos
$ cp triton-server-folder/common-repo/protobuf/*.proto ./Protos/
```

Make sure csproj has the newly added *.proto and then rebuild the solution:
```
  <ItemGroup>
    <Protobuf Include="Protos\grpc_service.proto" GrpcServices="Client" ProtoRoot="Protos\" />
    <Protobuf Include="Protos\health.proto" GrpcServices="Client" ProtoRoot="Protos\" />
    <Protobuf Include="Protos\model_config.proto" GrpcServices="Client" ProtoRoot="Protos\" />
  </ItemGroup>
```

Once compiled, one should notice the generated *.cs files (GrpcService.cs, GrpcServiceGrpc.cs, ModelConfig.cs, ModelConfigGrpc.cs, etc...) under obj folder, like obj\x64\Debug\net6.0. The C# example SimpleCSharpclient.cs shows details how to use it.

