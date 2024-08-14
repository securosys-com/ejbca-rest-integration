# EJBCA PKI [![Discuss](https://img.shields.io/badge/discuss-ejbca-ce?style=flat)](https://github.com/Keyfactor/ejbca-ce/discussions) 

EJBCA covers all your needs – from certificate management, registration and enrollment to certificate validation. 

Welcome to EJBCA – the Open Source Certificate Authority (software). EJBCA is one of the longest running CA software projects, providing time-proven robustness, reliability and flexibitlity. EJBCA is platform independent and can easily be scaled out to match the needs of your PKI requirements, whether you’re setting up a national eID, securing your industrial IoT platform or managing your own internal PKI for Enterprise or DevOps. 

EJBCA is developed in Java and runs on a JVM such as OpenJDK, available on most platforms such as Linux and Windows. 

There are two versions of EJBCA: 
* **EJBCA Community** (EJBCA CE) - free and open source, OSI Certified Open Source Software
* **EJBCA Enterprise** (EJBCA EE) - commercial and Common Criteria certified 

OSI Certified is a certification mark of the Open Source Initiative.

## Community Support

In our Community we welcome contributions. The Community software is open source and community supported, there is no support SLA, but a helpful best-effort Community.

* To report a problem or suggest a new feature, use the **[Issues](../../issues)** tab. 
* If you want to contribute actual bug fixes or proposed enhancements, use the **[Pull requests](../../pulls)** tab.
* Ask the community for ideas: **[EJBCA Discussions](https://github.com/Keyfactor/ejbca-ce/discussions)**.  
* Read more in our documentation: **[EJBCA Documentation](https://doc.primekey.com/ejbca)**.
* See release information: **[EJBCA Release information](https://doc.primekey.com/ejbca/ejbca-release-information)**. 
* Read more on the open source project website: **[EJBCA website](https://www.ejbca.org/)**.   


## License
EJBCA Community is licensed under the LGPL license, please see **[LICENSE](LICENSE)**. 

# EJBCA Rest Integration

This chapter will show you how to easily add Securosys Crypto Token support and HSM integration to your ejbca project.

## Get started 

To get started with **EJBCA Community**, clone **[ejbca-ce](https://github.com/Keyfactor/ejbca-ce)** and install it, see **[EJBCA Installation](https://doc.primekey.com/ejbca/ejbca-installation)**. 

You can also easily run EJBCA as a container from **[Dockerhub](https://hub.docker.com/r/keyfactor/ejbca-ce)**.

## Adding the Securosys Crypto Token Extension

All documentation on customizing ejbca configuration and adding own modifications can be found **[here](https://docs.keyfactor.com/ejbca/latest/handling-configurations-in-a-separate-directory)**.

In our case,in basic way, the following steps should be followed:

1. In the `ejbca-custom/conf` folder there are configuration files that you need to modify to your needs, such as `database.properties` etc. 
If you want to add the Securosys Crypto Token extension, make sure that the `securosys.cryptotoken.enabled=true` option is enabled in the `web.properties` file.

2. Insert the file ejbca-custom next into your EJBCA installation folder: `/opt/ejbca-custom`.

3. When you run `ant build` command inside an EJBCA installation folder, it will copy everything from ejbca-custom, replacing local files in the same location.

4. In the same directory run `ant deployear`.

5. Start ejbca.

## Create Securosys Crypto Token

In the EJBCA menu, under **CA Functions**, click **Crypto Tokens** to open the **Manage Crypto Tokens** page. Then click **Create new**.

Enter a **Name** and then select the type **Securosys Primus HSM**.

There are two ways for creating a Securosys Crypto Token connection with HSM (Authentication Type): **Bearer Token** or **mTLS certificate**.

1. **Bearer Token:**
 - In the **Securosys REST API URL** field, enter the endpoint to the TSB you want to connect to,
 - In the **Securosys REST API Bearer Token** field, enter your JWT bearer token.

2. **mTLS certificate:**
 - In the **Securosys REST API URL** field, enter the endpoint to the TSB you want to connect to,
 - Enter **mTLS certificate** and **mTLS key,**
 - Enter the appropriate **API Keys** to pass the authentication process for the individual operations that will be used on the crypto token after its creation. The **Management Key** and **Operation Key** are mandatory, while the **Service Key** is optional and will only be used to check the TSB version so that the appropriate operations are compatible with it. If you are using the latest available version of TSB, you can skip this key.

After clicking **Save** button, the **Securosys Crypto Token** will be created, which works on the same principles as other tokens.
