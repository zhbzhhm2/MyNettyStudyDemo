<h1 id="mynettylearn" style="box-sizing: border-box; margin: 0.8em 0px; font-size: 28px; font-family: &quot;Microsoft YaHei&quot;; font-weight: 100; line-height: 30px; color: rgb(102, 102, 102); padding: 0px; border: 0px; outline: 0px; vertical-align: baseline; background: transparent;">
	MyNettyLearn
</h1>
<ul style="box-sizing: border-box; margin: 0px 0px 22px; padding: 0px; font-family: &quot;Microsoft YaHei&quot;; list-style: square inside; border: 0px; outline: 0px; font-size: 14px; vertical-align: baseline; background: transparent; color: rgb(153, 153, 153);">
	<li style="box-sizing: border-box; margin: 0px; padding: 0px; list-style: none; border: 0px; outline: 0px; vertical-align: baseline; background: transparent;">
		使用Netty完成网络通讯的常用功能&nbsp;<br style="box-sizing: border-box;" />
		-这里的常用功能包括：&nbsp;<br style="box-sizing: border-box;" />
		1.文本的传输&nbsp;<br style="box-sizing: border-box;" />
		2.二进制文件的传输&nbsp;<br style="box-sizing: border-box;" />
		3.进程之间的参数传递
	</li>
	<li style="box-sizing: border-box; margin: 0px; padding: 0px; list-style: none; border: 0px; outline: 0px; vertical-align: baseline; background: transparent;">
		<p style="box-sizing: border-box; margin-top: 0px; margin-bottom: 1.1em; padding-top: 0px; padding-bottom: 0px; border: 0px; outline: 0px; font-size: 15px; vertical-align: baseline; background: transparent; color: rgb(102, 102, 102); line-height: 26px;">
			一、功能规划
		</p>
		<blockquote style="box-sizing: border-box; padding: 15px 20px; margin: 0px 0px 1.1em; border-width: 0px 0px 0px 10px; border-left-style: solid; border-left-color: rgba(128, 128, 128, 0.0745098); border-top-style: initial; border-right-style: initial; border-bottom-style: initial; border-top-color: initial; border-right-color: initial; border-bottom-color: initial; border-image: initial; outline: 0px; vertical-align: baseline; background: rgba(128, 128, 128, 0.0470588); border-radius: 0px 5px 5px 0px;">
			<p style="box-sizing: border-box; margin-top: 0px; margin-bottom: 0px; padding-top: 0px; padding-bottom: 0px; border: 0px; outline: 0px; font-size: 15px; vertical-align: baseline; background: transparent; line-height: 1.25; color: rgb(102, 102, 102);">
				1.客户端向服务器询问指定语句，服务器从数据库中查询后向客户端返回指定语句&nbsp;<br style="box-sizing: border-box;" />
				2.客户端向服务器询问指定文件，服务器返回指定文件&nbsp;<br style="box-sizing: border-box;" />
				3.客户端向服务器请求某种资源，服务器查看资源是否足够，向客户端提供资源&nbsp;<br style="box-sizing: border-box;" />
				4.客户端向服务器归还资源
			</p>
		</blockquote>
	</li>
	<li style="box-sizing: border-box; margin: 0px; padding: 0px; list-style: none; border: 0px; outline: 0px; vertical-align: baseline; background: transparent;">
		<p style="box-sizing: border-box; margin-top: 0px; margin-bottom: 1.1em; padding-top: 0px; padding-bottom: 0px; border: 0px; outline: 0px; font-size: 15px; vertical-align: baseline; background: transparent; color: rgb(102, 102, 102); line-height: 26px;">
			二、通信包结构&nbsp;<br style="box-sizing: border-box;" />
			请求包
		</p>
		<blockquote style="box-sizing: border-box; padding: 15px 20px; margin: 0px 0px 1.1em; border-width: 0px 0px 0px 10px; border-left-style: solid; border-left-color: rgba(128, 128, 128, 0.0745098); border-top-style: initial; border-right-style: initial; border-bottom-style: initial; border-top-color: initial; border-right-color: initial; border-bottom-color: initial; border-image: initial; outline: 0px; vertical-align: baseline; background: rgba(128, 128, 128, 0.0470588); border-radius: 0px 5px 5px 0px;">
			<table style="box-sizing: border-box; border-collapse: collapse; border-spacing: 0px; max-width: 100%; background: transparent; margin: 0px; padding: 0px; border: 1px solid rgb(238, 238, 238); outline: 0px; font-size: 14px; vertical-align: baseline; width: 604px;">
				<thead style="box-sizing: border-box; margin: 0px; padding: 0px; border: 0px; outline: 0px; vertical-align: baseline; background: transparent;">
					<tr style="box-sizing: border-box; margin: 0px; padding: 0px; border: 0px; outline: 0px; vertical-align: baseline; background: transparent;">
						<th align="center" style="box-sizing: border-box; text-align: left; margin: 0px; padding: 8px; border: 1px solid rgb(238, 238, 238); outline: 0px; font-size: 14px; vertical-align: top; background: transparent; line-height: 20px;">
							请求编号ID(4B)
						</th>
						<th align="center" style="box-sizing: border-box; text-align: left; margin: 0px; padding: 8px; border: 1px solid rgb(238, 238, 238); outline: 0px; font-size: 14px; vertical-align: top; background: transparent; line-height: 20px;">
							请求代码(4B)
						</th>
						<th align="center" style="box-sizing: border-box; text-align: left; margin: 0px; padding: 8px; border: 1px solid rgb(238, 238, 238); outline: 0px; font-size: 14px; vertical-align: top; background: transparent; line-height: 20px;">
							请求内容
						</th>
					</tr>
				</thead>
			</table>
		</blockquote>
		<p style="box-sizing: border-box; margin-top: 0px; margin-bottom: 1.1em; padding-top: 0px; padding-bottom: 0px; border: 0px; outline: 0px; font-size: 15px; vertical-align: baseline; background: transparent; color: rgb(102, 102, 102); line-height: 26px;">
			响应包
		</p>
		<blockquote style="box-sizing: border-box; padding: 15px 20px; margin: 0px 0px 1.1em; border-width: 0px 0px 0px 10px; border-left-style: solid; border-left-color: rgba(128, 128, 128, 0.0745098); border-top-style: initial; border-right-style: initial; border-bottom-style: initial; border-top-color: initial; border-right-color: initial; border-bottom-color: initial; border-image: initial; outline: 0px; vertical-align: baseline; background: rgba(128, 128, 128, 0.0470588); border-radius: 0px 5px 5px 0px;">
			<table style="box-sizing: border-box; border-collapse: collapse; border-spacing: 0px; max-width: 100%; background: transparent; margin: 0px; padding: 0px; border: 1px solid rgb(238, 238, 238); outline: 0px; font-size: 14px; vertical-align: baseline; width: 604px;">
				<thead style="box-sizing: border-box; margin: 0px; padding: 0px; border: 0px; outline: 0px; vertical-align: baseline; background: transparent;">
					<tr style="box-sizing: border-box; margin: 0px; padding: 0px; border: 0px; outline: 0px; vertical-align: baseline; background: transparent;">
						<th align="center" style="box-sizing: border-box; text-align: left; margin: 0px; padding: 8px; border: 1px solid rgb(238, 238, 238); outline: 0px; font-size: 14px; vertical-align: top; background: transparent; line-height: 20px;">
							响应编号ID(4B)
						</th>
						<th align="center" style="box-sizing: border-box; text-align: left; margin: 0px; padding: 8px; border: 1px solid rgb(238, 238, 238); outline: 0px; font-size: 14px; vertical-align: top; background: transparent; line-height: 20px;">
							响应代码(4B)
						</th>
						<th align="center" style="box-sizing: border-box; text-align: left; margin: 0px; padding: 8px; border: 1px solid rgb(238, 238, 238); outline: 0px; font-size: 14px; vertical-align: top; background: transparent; line-height: 20px;">
							响应内容
						</th>
					</tr>
				</thead>
			</table>
		</blockquote>
		<p style="box-sizing: border-box; margin-top: 0px; margin-bottom: 1.1em; padding-top: 0px; padding-bottom: 0px; border: 0px; outline: 0px; font-size: 15px; vertical-align: baseline; background: transparent; color: rgb(102, 102, 102); line-height: 26px;">
			备注
		</p>
		<blockquote style="box-sizing: border-box; padding: 15px 20px; margin: 0px 0px 1.1em; border-width: 0px 0px 0px 10px; border-left-style: solid; border-left-color: rgba(128, 128, 128, 0.0745098); border-top-style: initial; border-right-style: initial; border-bottom-style: initial; border-top-color: initial; border-right-color: initial; border-bottom-color: initial; border-image: initial; outline: 0px; vertical-align: baseline; background: rgba(128, 128, 128, 0.0470588); border-radius: 0px 5px 5px 0px;">
			<p style="box-sizing: border-box; margin-top: 0px; margin-bottom: 1.1em; padding-top: 0px; padding-bottom: 0px; border: 0px; outline: 0px; font-size: 15px; vertical-align: baseline; background: transparent; line-height: 1.25; color: rgb(102, 102, 102);">
				1.请求编号是指请求的顺序，在一次应答中，响应编号与请求编号相同&nbsp;<br style="box-sizing: border-box;" />
				2.请求代码
			</p>
			<blockquote style="box-sizing: border-box; padding: 15px 20px; margin: 0px 0px 1.1em; border-width: 0px 0px 0px 10px; border-left-style: solid; border-left-color: rgba(128, 128, 128, 0.0745098); border-top-style: initial; border-right-style: initial; border-bottom-style: initial; border-top-color: initial; border-right-color: initial; border-bottom-color: initial; border-image: initial; outline: 0px; vertical-align: baseline; background-image: initial; background-position: initial; background-size: initial; background-repeat: initial; background-attachment: initial; background-origin: initial; background-clip: initial; border-radius: 0px 5px 5px 0px;">
				<table style="box-sizing: border-box; border-collapse: collapse; border-spacing: 0px; max-width: 100%; background: transparent; margin: 0px; padding: 0px; border: 1px solid rgb(238, 238, 238); outline: 0px; font-size: 14px; vertical-align: baseline; width: 554px;">
					<thead style="box-sizing: border-box; margin: 0px; padding: 0px; border: 0px; outline: 0px; vertical-align: baseline; background: transparent;">
						<tr style="box-sizing: border-box; margin: 0px; padding: 0px; border: 0px; outline: 0px; vertical-align: baseline; background: transparent;">
							<th align="center" style="box-sizing: border-box; text-align: left; margin: 0px; padding: 8px; border: 1px solid rgb(238, 238, 238); outline: 0px; font-size: 14px; vertical-align: top; background: transparent; line-height: 20px;">
								0
							</th>
							<th style="box-sizing: border-box; text-align: left; margin: 0px; padding: 8px; border: 1px solid rgb(238, 238, 238); outline: 0px; font-size: 14px; vertical-align: top; background: transparent; line-height: 20px;">
								查询指定语句
							</th>
						</tr>
					</thead>
					<tbody style="box-sizing: border-box; margin: 0px; padding: 0px; border: 0px; outline: 0px; vertical-align: baseline; background: transparent;">
						<tr style="box-sizing: border-box; margin: 0px; padding: 0px; border: 0px; outline: 0px; vertical-align: baseline; background: transparent;">
							<td align="center" style="box-sizing: border-box; margin: 0px; padding: 8px; border: 1px solid rgb(238, 238, 238); outline: 0px; font-size: 14px; vertical-align: top; background: transparent; line-height: 20px;">
								1
							</td>
							<td style="box-sizing: border-box; margin: 0px; padding: 8px; border: 1px solid rgb(238, 238, 238); outline: 0px; font-size: 14px; vertical-align: top; background: transparent; line-height: 20px;">
								申请指定文件
							</td>
						</tr>
						<tr style="box-sizing: border-box; margin: 0px; padding: 0px; border: 0px; outline: 0px; vertical-align: baseline; background: transparent;">
							<td align="center" style="box-sizing: border-box; margin: 0px; padding: 8px; border: 1px solid rgb(238, 238, 238); outline: 0px; font-size: 14px; vertical-align: top; background: transparent; line-height: 20px;">
								2
							</td>
							<td style="box-sizing: border-box; margin: 0px; padding: 8px; border: 1px solid rgb(238, 238, 238); outline: 0px; font-size: 14px; vertical-align: top; background: transparent; line-height: 20px;">
								请求指定资源
							</td>
						</tr>
						<tr style="box-sizing: border-box; margin: 0px; padding: 0px; border: 0px; outline: 0px; vertical-align: baseline; background: transparent;">
							<td align="center" style="box-sizing: border-box; margin: 0px; padding: 8px; border: 1px solid rgb(238, 238, 238); outline: 0px; font-size: 14px; vertical-align: top; background: transparent; line-height: 20px;">
								3
							</td>
							<td style="box-sizing: border-box; margin: 0px; padding: 8px; border: 1px solid rgb(238, 238, 238); outline: 0px; font-size: 14px; vertical-align: top; background: transparent; line-height: 20px;">
								归还指定资源
							</td>
						</tr>
					</tbody>
				</table>
			</blockquote>
			<p style="box-sizing: border-box; margin-top: 0px; margin-bottom: 1.1em; padding-top: 0px; padding-bottom: 0px; border: 0px; outline: 0px; font-size: 15px; vertical-align: baseline; background: transparent; line-height: 1.25; color: rgb(102, 102, 102);">
				3.响应代码
			</p>
			<blockquote style="box-sizing: border-box; padding: 15px 20px; margin: 0px 0px 1.1em; border-width: 0px 0px 0px 10px; border-left-style: solid; border-left-color: rgba(128, 128, 128, 0.0745098); border-top-style: initial; border-right-style: initial; border-bottom-style: initial; border-top-color: initial; border-right-color: initial; border-bottom-color: initial; border-image: initial; outline: 0px; vertical-align: baseline; background-image: initial; background-position: initial; background-size: initial; background-repeat: initial; background-attachment: initial; background-origin: initial; background-clip: initial; border-radius: 0px 5px 5px 0px;">
				<table style="box-sizing: border-box; border-collapse: collapse; border-spacing: 0px; max-width: 100%; background: transparent; margin: 0px; padding: 0px; border: 1px solid rgb(238, 238, 238); outline: 0px; font-size: 14px; vertical-align: baseline; width: 554px;">
					<thead style="box-sizing: border-box; margin: 0px; padding: 0px; border: 0px; outline: 0px; vertical-align: baseline; background: transparent;">
						<tr style="box-sizing: border-box; margin: 0px; padding: 0px; border: 0px; outline: 0px; vertical-align: baseline; background: transparent;">
							<th align="center" style="box-sizing: border-box; text-align: left; margin: 0px; padding: 8px; border: 1px solid rgb(238, 238, 238); outline: 0px; font-size: 14px; vertical-align: top; background: transparent; line-height: 20px;">
								100
							</th>
							<th style="box-sizing: border-box; text-align: left; margin: 0px; padding: 8px; border: 1px solid rgb(238, 238, 238); outline: 0px; font-size: 14px; vertical-align: top; background: transparent; line-height: 20px;">
								应答指定语句
							</th>
						</tr>
					</thead>
					<tbody style="box-sizing: border-box; margin: 0px; padding: 0px; border: 0px; outline: 0px; vertical-align: baseline; background: transparent;">
						<tr style="box-sizing: border-box; margin: 0px; padding: 0px; border: 0px; outline: 0px; vertical-align: baseline; background: transparent;">
							<td align="center" style="box-sizing: border-box; margin: 0px; padding: 8px; border: 1px solid rgb(238, 238, 238); outline: 0px; font-size: 14px; vertical-align: top; background: transparent; line-height: 20px;">
								101
							</td>
							<td style="box-sizing: border-box; margin: 0px; padding: 8px; border: 1px solid rgb(238, 238, 238); outline: 0px; font-size: 14px; vertical-align: top; background: transparent; line-height: 20px;">
								返回指定文件
							</td>
						</tr>
						<tr style="box-sizing: border-box; margin: 0px; padding: 0px; border: 0px; outline: 0px; vertical-align: baseline; background: transparent;">
							<td align="center" style="box-sizing: border-box; margin: 0px; padding: 8px; border: 1px solid rgb(238, 238, 238); outline: 0px; font-size: 14px; vertical-align: top; background: transparent; line-height: 20px;">
								102
							</td>
							<td style="box-sizing: border-box; margin: 0px; padding: 8px; border: 1px solid rgb(238, 238, 238); outline: 0px; font-size: 14px; vertical-align: top; background: transparent; line-height: 20px;">
								同意申请指定资源
							</td>
						</tr>
						<tr style="box-sizing: border-box; margin: 0px; padding: 0px; border: 0px; outline: 0px; vertical-align: baseline; background: transparent;">
							<td align="center" style="box-sizing: border-box; margin: 0px; padding: 8px; border: 1px solid rgb(238, 238, 238); outline: 0px; font-size: 14px; vertical-align: top; background: transparent; line-height: 20px;">
								502
							</td>
							<td style="box-sizing: border-box; margin: 0px; padding: 8px; border: 1px solid rgb(238, 238, 238); outline: 0px; font-size: 14px; vertical-align: top; background: transparent; line-height: 20px;">
								拒绝申请指定资源
							</td>
						</tr>
						<tr style="box-sizing: border-box; margin: 0px; padding: 0px; border: 0px; outline: 0px; vertical-align: baseline; background: transparent;">
							<td align="center" style="box-sizing: border-box; margin: 0px; padding: 8px; border: 1px solid rgb(238, 238, 238); outline: 0px; font-size: 14px; vertical-align: top; background: transparent; line-height: 20px;">
								103
							</td>
							<td style="box-sizing: border-box; margin: 0px; padding: 8px; border: 1px solid rgb(238, 238, 238); outline: 0px; font-size: 14px; vertical-align: top; background: transparent; line-height: 20px;">
								同意归还指定资源
							</td>
						</tr>
					</tbody>
				</table>
			</blockquote>
		</blockquote>
	</li>
</ul>
